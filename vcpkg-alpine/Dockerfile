FROM wangq/alpine:master
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

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
    && eza -T -L 1 /opt/vcpkg

RUN true \
    && echo 'set(VCPKG_TARGET_ARCHITECTURE x64)' > /opt/vcpkg/triplets/community/x64-linux-musl.cmake \
    && echo 'set(VCPKG_CRT_LINKAGE static)' >> /opt/vcpkg/triplets/community/x64-linux-musl.cmake \
    && echo 'set(VCPKG_LIBRARY_LINKAGE static)' >> /opt/vcpkg/triplets/community/x64-linux-musl.cmake \
    && echo '' >> /opt/vcpkg/triplets/community/x64-linux-musl.cmake \
    && echo 'set(VCPKG_CMAKE_SYSTEM_NAME Linux)' >> /opt/vcpkg/triplets/community/x64-linux-musl.cmake \
    && echo 'set(VCPKG_BUILD_TYPE release)' >> /opt/vcpkg/triplets/community/x64-linux-musl.cmake
