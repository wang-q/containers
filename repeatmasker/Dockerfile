FROM wangq/base:master
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

RUN true \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        hmmer \
        trf \
        tree

# rmblast
RUN true \
    && curl -L https://www.repeatmasker.org/rmblast/rmblast-2.14.1+-x64-linux-GLIBC_2.31.tar.gz | tar xz \
    && tree /app

# RepeatMasker
RUN true \
    && curl -L https://repeatmasker.org/RepeatMasker/RepeatMasker-4.1.1.tar.gz | tar xz \
    && tree /app

