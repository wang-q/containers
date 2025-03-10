FROM centos:7

RUN true \
    && yum -y --setopt=tsflags=nodocs update \
    && yum -y groupinstall 'Development Tools' \
    && yum -y install file vim \
    && yum -y install curl zip unzip tar \
    && yum -y install autoconf automake autoconf-archive libtool-ltdl-devel \
    && mkdir -p app

WORKDIR /app
