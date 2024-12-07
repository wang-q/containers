FROM wangq/brew:master
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

ENV PATH="/home/linuxbrew/share/Perl/bin:${PATH}"

RUN true \
    && mkdir -p /home/linuxbrew/share/Perl \
    && curl -L https://www.cpan.org/src/5.0/perl-5.34.3.tar.gz | tar xz \
    && cd perl-5.34.3 \
    && ./Configure \
        -des \
        -Dprefix=/home/linuxbrew/share/Perl \
        -Dcc=gcc \
        -Duseshrplib \
        -Duselargefiles \
        -Dusethreads \
    && make -j 2 \
    && make install \
    && cd .. \
    && rm -fr perl-5.34.3 \
    && perl -v \
    && curl -L https://cpanmin.us | perl - App::cpanminus \
    && cpanm -nq Text::Soundex

ENV PATH="/home/linuxbrew/share/Python/bin:${PATH}"

RUN true \
    && mkdir -p /home/linuxbrew/share/Python \
    && curl -L https://www.python.org/ftp/python/3.10.16/Python-3.10.16.tar.xz | tar xJ \
    && cd Python-3.10.16 \
    && CC=gcc ./configure \
        --prefix=/home/linuxbrew/share/Python \
        --enable-optimizations \
        --enable-ipv6 \
        --enable-loadable-sqlite-extensions \
        --with-lto \
    && make -j 2 \
    && make install \
    && cd .. \
    && rm -fr Python-3.10.16 \
    && python3 -V \
    && pip3 install --upgrade pip setuptools wheel pysocks \
    && pip3 install h5py
