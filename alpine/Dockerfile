FROM alpine:3.21
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

RUN true \
    && apk update \
    && apk upgrade \
    && apk add --no-cache \
        build-base \
        openssh \
        zip \
        unzip \
        linux-headers \
        cmake \
        git \
        binutils \
        perl \
        python3 \
        curl \
        re2c \
        flex \
        bison \
        meson \
        pkgconf \
        bash \
        openssl-dev \
        gettext-dev \
        tree

RUN true \
    && curl -L https://github.com/ninja-build/ninja/archive/refs/tags/v1.12.1.tar.gz \
        | tar xz \
    && mv ninja-* ninja \
    && cd ninja \
    && cmake -S. -B build \
    && cmake --build build \
    && cmake --install build \
    && cd .. \
    && rm -rf ninja \
    && ninja --version
