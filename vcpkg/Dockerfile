FROM wangq/base:master
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

RUN true \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        zip \
        unzip \
        tar \
        cmake \
        ninja \
        meson \
        autoconf \
        automake \
        libtool \
        libltdl-dev \
        tree \
    && apt-get autoremove --purge -y \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir -p app

ENV VCPKG_ROOT=/app/vcpkg
ENV PATH=$VCPKG_ROOT:$PATH

RUN true \
    && curl -L https://github.com/microsoft/vcpkg/archive/refs/tags/2025.02.14.tar.gz \
        | tar xz \
    && mv vcpkg-* /app/vcpkg \
    && cd /app/vcpkg \
    && ./bootstrap-vcpkg.sh -disableMetrics -musl \
    && tree /app

WORKDIR /app
