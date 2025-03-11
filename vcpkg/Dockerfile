FROM centos:7

ARG minorver=7.9.2009

RUN true \
    && sed -i.bak -e "s|^mirrorlist=|#mirrorlist=|g" \
        -e "s|^#baseurl=http://mirror.centos.org/centos/\$releasever|baseurl=https://vault.centos.org/$minorver|g" \
        /etc/yum.repos.d/CentOS-*.repo \
    && yum -y --setopt=tsflags=nodocs update \
    && yum -y groupinstall 'Development Tools' \
    && yum -y install file vim \
    && yum -y install curl zip unzip tar \
    && yum -y install autoconf automake autoconf-archive libtool-ltdl-devel \
    && yum -y install openssl-devel bzip2-devel libffi-devel sqlite-devel \
    && rpm -U http://opensource.wandisco.com/centos/7/git/x86_64/wandisco-git-release-7-2.noarch.rpm \
    && yum -y install git \
    && yum clean all \
    && rm -rf /var/cache/yum/* \
    && rm -rf var/lib/yum/yumdb/*

RUN true \
    && curl -LO https://raw.githubusercontent.com/wang-q/dotfiles/refs/heads/master/python/build.sh \
    && bash build.sh \
    && ln -sf $HOME/share/Python/bin/python3 /usr/bin/python3 \
    && ln -sf $HOME/share/Python/bin/pip3 /usr/bin/pip3 \
    && ln -sf $HOME/share/Python/bin/python3-config /usr/bin/python3-config \
    && python3 -V


ENV PATH=/opt/cbp/bin:$PATH

RUN true \
    && curl -LO https://github.com/wang-q/cbp/releases/latest/download/cbp.linux \
    && chmod +x cbp.linux \
    && ./cbp.linux init --dev /opt/cbp \
    && rm ./cbp.linux \
    && /root/.cbp/bin/cbp install cmake ninja jq eza

ENV VCPKG_FORCE_SYSTEM_BINARIES=1
ENV VCPKG_ROOT=/opt/vcpkg
ENV PATH=$VCPKG_ROOT:$PATH

RUN true \
    && mkdir -p /opt \
    && curl -L https://github.com/microsoft/vcpkg/archive/refs/tags/2025.02.14.tar.gz \
        | tar xz \
    && mv vcpkg-* /opt/vcpkg \
    && cd /opt/vcpkg \
    && ./bootstrap-vcpkg.sh -disableMetrics \
    && eza -T -L 1 /opt/vcpkg \
    && eza -T -L 1 /opt/cbp/bin
