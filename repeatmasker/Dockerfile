FROM wangq/base:master
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

# RepeatMasker
RUN true \
    && apt-get update \
    && apt-get install -y --no-install-recommends `# brew` \
    && hmmer \
    && trf

# rmblast
RUN true \
    && curl -L https://www.repeatmasker.org/rmblast/rmblast-2.14.1+-x64-linux-GLIBC_2.31.tar.gz | tar xz \
    && ls

