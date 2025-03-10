FROM centos:7

ARG minorver=7.9.2009
ARG VCPKG_ROOT=/app/vcpkg
ARG PATH=$VCPKG_ROOT:$PATH

RUN true \
    && sed -i.bak -e "s|^mirrorlist=|#mirrorlist=|g" \
        -e "s|^#baseurl=http://mirror.centos.org/centos/\$releasever|baseurl=https://vault.centos.org/$minorver|g" \
        /etc/yum.repos.d/CentOS-*.repo \
    && yum -y --setopt=tsflags=nodocs update \
    && yum -y groupinstall 'Development Tools' \
    && yum -y install file vim \
    && yum -y install curl zip unzip tar \
    && yum -y install autoconf automake autoconf-archive libtool-ltdl-devel \
    && yum clean all

RUN true \
    && mkdir -p /app \
    && curl -L https://github.com/microsoft/vcpkg/archive/refs/tags/2025.02.14.tar.gz \
        | tar xz \
    && mv vcpkg-* /app/vcpkg \
    && cd /app/vcpkg \
    && ./bootstrap-vcpkg.sh -disableMetrics -musl

WORKDIR /app
