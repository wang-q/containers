FROM centos:7
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

ARG minorver=7.9.2009

RUN true \
    && sed -i.bak -e "s|^mirrorlist=|#mirrorlist=|g" \
        -e "s|^#baseurl=http://mirror.centos.org/centos/\$releasever|baseurl=https://vault.centos.org/$minorver|g" \
        /etc/yum.repos.d/CentOS-*.repo \
    && yum -y --setopt=tsflags=nodocs update \
    && yum -y groupinstall 'Development Tools' \
    && yum -y install net-tools file vim \
    && yum -y install curl zip unzip tar \
    && yum -y install zlib-devel bzip2-devel xz-devel \
    && yum -y install autoconf automake autoconf-archive libtool-ltdl-devel \
    && yum -y install ncurses-devel readline-devel \
    && yum -y install libxml2-devel expat-devel pcre-devel pcre2-devel \
    && yum -y install openssl-devel libcurl-devel \
    && yum -y install libffi-devel libuuid-devel sqlite-devel \
    && yum -y install blas-devel lapack-devel \
    && yum -y install libpng-devel libjpeg-turbo-devel libtiff-devel \
    && yum -y install freetype-devel fontconfig-devel \
    && yum -y install perl-ExtUtils-MakeMaker perl-Test-Simple perl-IPC-Cmd perl-Digest-MD5 \
    && rpm -U http://opensource.wandisco.com/centos/7/git/x86_64/wandisco-git-release-7-2.noarch.rpm \
    && yum -y install git \
    && yum clean all \
    && rm -rf /var/cache/yum/* \
    && rm -rf var/lib/yum/yumdb/*
