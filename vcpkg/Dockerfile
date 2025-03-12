FROM alpine:3.21

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
        flex \
        bison \
        meson \
        pkgconf \
        bash \
        openssl-dev \
        tree

ENV PATH=/opt/cbp/bin:$PATH

RUN true \
    && curl -LO https://github.com/wang-q/cbp/releases/latest/download/cbp.linux \
    && chmod +x cbp.linux \
    && ./cbp.linux init --dev /opt/cbp \
    && rm ./cbp.linux \
    && /root/.cbp/bin/cbp install ninja jq eza

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
    && eza -T -L 1 /opt/vcpkg \
    && eza -T -L 1 /opt/cbp/bin

RUN true \
    && echo 'set(VCPKG_TARGET_ARCHITECTURE x64)' > /opt/vcpkg/triplets/community/x64-linux-musl.cmake \
    && echo 'set(VCPKG_CRT_LINKAGE static)' >> /opt/vcpkg/triplets/community/x64-linux-musl.cmake \
    && echo 'set(VCPKG_LIBRARY_LINKAGE static)' >> /opt/vcpkg/triplets/community/x64-linux-musl.cmake \
    && echo '' >> /opt/vcpkg/triplets/community/x64-linux-musl.cmake \
    && echo 'set(VCPKG_CMAKE_SYSTEM_NAME Linux)' >> /opt/vcpkg/triplets/community/x64-linux-musl.cmake \
    && echo 'set(VCPKG_BUILD_TYPE release)' >> /opt/vcpkg/triplets/community/x64-linux-musl.cmake
