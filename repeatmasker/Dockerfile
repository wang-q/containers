FROM wangq/base:master
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

RUN true \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        hmmer \
        trf \
        tree \
    && mkdir -p app

RUN true \
    && cpanm -nq Text::Soundex \
    && pip3 install h5py

# rmblast
RUN true \
    && curl -L https://www.repeatmasker.org/rmblast/rmblast-2.14.1+-x64-linux-GLIBC_2.31.tar.gz \
        | tar xz \
    && tree /app

# /app/RepeatMasker/RepeatMasker
# The RepeatMasker configure script must be run from inside the RepeatMasker installation directory
RUN true \
    && curl -L https://repeatmasker.org/RepeatMasker/RepeatMasker-4.1.1.tar.gz \
        | tar xz \
    && cd /app/RepeatMasker \
    && perl configure \
        -hmmer_dir=/usr/bin \
        -trf_prgm=/usr/bin/trf \
        -rmblast_dir=/app/rmblast-2.14.1/bin \
        -libdir=/app/RepeatMasker/Libraries \
        -default_search_engine=rmblast
