FROM centos:7

ARG minorver=7.9.2009
ENV VCPKG_ROOT=/app/vcpkg
ENV PATH=$VCPKG_ROOT:$PATH

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
    && python3 -V

RUN true \
    && mkdir -p /app \
    && curl -L https://github.com/microsoft/vcpkg/archive/refs/tags/2025.02.14.tar.gz \
        | tar xz \
    && mv vcpkg-* /app/vcpkg \
    && cd /app/vcpkg \
    && ./bootstrap-vcpkg.sh -disableMetrics

WORKDIR /app
