FROM wangq/ubuntu:master
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

RUN true \
    && apt-get update \
    && apt-get install -y --no-install-recommends perl cpanminus python3 python3-pip python3-pip-whl \
    && apt-get install -y --no-install-recommends \
        hmmer \
        trf \
        tree \
    && apt-get autoremove --purge -y \
    && rm -rf /var/lib/apt/lists/* \

RUN true \
    && cpanm -nq Text::Soundex \
    && pip3 install h5py \
    && mkdir -p /opt

WORKDIR /opt

# rmblast
RUN true \
    && curl -L https://www.repeatmasker.org/rmblast/rmblast-2.14.1+-x64-linux-GLIBC_2.31.tar.gz \
        | tar xz \
    && mv rmblast-* /opt/rmblast \
    && tree /opt

# /app/RepeatMasker/RepeatMasker
# The RepeatMasker configure script must be run from inside the RepeatMasker installation directory
RUN true \
    && curl -L https://repeatmasker.org/RepeatMasker/RepeatMasker-4.1.1.tar.gz \
        | tar xz \
    && cd /opt/RepeatMasker \
    && perl configure \
        -hmmer_dir=/usr/bin \
        -trf_prgm=/usr/bin/trf \
        -rmblast_dir=/opt/rmblast/bin \
        -libdir=/opt/RepeatMasker/Libraries \
        -default_search_engine=rmblast
