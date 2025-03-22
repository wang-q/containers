FROM wangq/centos:master
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

ENV PATH=/opt/Python/bin:$PATH

RUN true \
    && curl -L https://mirrors.huaweicloud.com/python/3.9.21/Python-3.9.21.tgz \
        | tar xz \
    && cd Python-* \
    && ./configure \
        --prefix=/opt/Python \
        --enable-optimizations \
        --enable-ipv6 \
        --enable-loadable-sqlite-extensions \
        --with-lto \
    && make -j 2 \
    && make install \
    && cd .. \
    && rm -rf Python-* \
    && python3 -V

RUN true \
    && pip3 install \
        --trusted-host mirror.nju.edu.cn \
        -i http://mirror.nju.edu.cn/pypi/web/simple/ \
        --upgrade pip setuptools wheel pysocks meson

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
    && eza -T -L 1 /opt/Python/bin \
    && eza -T -L 1 /opt/cbp/bin \
    && eza -T -L 1 /opt/vcpkg
