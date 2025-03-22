FROM wangq/ubuntu:master
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

RUN true \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        zip \
        unzip \
        tar \
        pkg-config \
        cmake \
        ninja-build \
        meson \
        autoconf \
        automake \
        libtool \
        libltdl-dev \
        bison \
        flex \
        tree \
    && apt-get autoremove --purge -y \
    && rm -rf /var/lib/apt/lists/*

ENV PATH=/opt/cbp/bin:$PATH

RUN true \
    && mkdir -p /opt \
    && curl -LO https://github.com/wang-q/cbp/releases/latest/download/cbp.linux \
    && chmod +x cbp.linux \
    && ./cbp.linux init --dev /opt/cbp \
    && rm ./cbp.linux \
    && /opt/cbp/bin/cbp install cmake ninja jq eza

ENV VCPKG_FORCE_SYSTEM_BINARIES=1
ENV VCPKG_ROOT=/opt/vcpkg
ENV PATH=$VCPKG_ROOT:$PATH

RUN true \
    && curl -L https://github.com/microsoft/vcpkg/archive/refs/tags/2025.02.14.tar.gz \
        | tar xz \
    && mv vcpkg-* /opt/vcpkg \
    && cd /opt/vcpkg \
    && ./bootstrap-vcpkg.sh -disableMetrics

RUN true \
    && eza -T -L 1 /opt/cbp/bin \
    && eza -T -L 1 /opt/vcpkg
