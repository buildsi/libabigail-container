ARG fedora_version
FROM fedora:${fedora_version} as builder

# docker build -f docker/Dockerfile.fedora-base -t ghcr.io/woodard/libabigail-fedora-base .

ARG LIBRARY_VERSION=2.0
RUN dnf install -y \
    autoconf \
    automake \
    cpio \
    elfutils-devel \
    gcc-c++ \
    lbzip2 \
    libtool \
    libxml2-devel \
    python3-koji \
    python3-mock \
    python3-pyxdg \
    shared-mime-info \
    six \
    wget

RUN dnf install -y redhat-rpm-config || echo "Not in distribution"
RUN ldconfig && \ 
    wget http://mirrors.kernel.org/sourceware/libabigail/libabigail-${LIBRARY_VERSION}.tar.gz && \
    tar -xvf libabigail-${LIBRARY_VERSION}.tar.gz && \
    cd libabigail-${LIBRARY_VERSION} && \
    mkdir -p build && \
    autoreconf -i && \
    cd build && \
    CXXFLAGS="-g3 -fvar-tracking-assignments \
    -gstatement-frontiers -gvariable-location-views -grecord-gcc-switches -pipe -Wall \
    -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -Wp,-D_GLIBCXX_ASSERTIONS \
    -fstack-protector-strong -fstack-clash-protection -fcf-protection \
    -fasynchronous-unwind-tables -O2" CFLAGS="-g3 -fvar-tracking-assignments \
    -gstatement-frontiers -gvariable-location-views -grecord-gcc-switches -pipe -Wall \
    -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -Wp,-D_GLIBCXX_ASSERTIONS \
    -fstack-protector-strong -fstack-clash-protection -fcf-protection \
    -fasynchronous-unwind-tables -O2" LDFLAGS="-Wl,--no-undefined" \
    ../configure --prefix=/opt/libabigail --enable-rpm=yes && \
    make -j4 && \
    make install

ENV PATH=/opt/libabigail/bin:$PATH

# Runtime dependencies
RUN dnf install -y \
    python3-koji \
    python3-mock \
    python3-pyxdg \
    elfutils-libelf \
    elfutils-libs \
    libstdc++ \
    lbzip2 \
    shared-mime-info \
    six
