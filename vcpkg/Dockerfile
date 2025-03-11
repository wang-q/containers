FROM alpine:3.21

RUN true \
    && apk update \
    && apk upgrade \
    && apk add \
        build-base \
        openssh \
        zip \
        unzip \
        linux-headers \
        cmake \
        git \
        binutils \
        perl \
        curl \
        flex \
        bison \
        ninja \
        pkgconf \
        bash \
        openssl-dev \
        tree

ENV VCPKG_FORCE_SYSTEM_BINARIES 1
ENV VCPKG_ROOT /opt/vcpkg
ENV PATH=$VCPKG_ROOT:$PATH

RUN true \
    && curl -L https://github.com/microsoft/vcpkg/archive/refs/tags/2025.02.14.tar.gz \
        | tar xz \
    && mv vcpkg-* /opt/vcpkg \
    && cd /opt/vcpkg \
    && ./bootstrap-vcpkg.sh -disableMetrics -musl \
    && tree /opt/vcpkg
