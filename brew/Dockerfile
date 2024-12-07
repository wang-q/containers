ARG version=22.04
# version is passed through by Docker.
# shellcheck disable=SC2154
FROM ubuntu:"${version}"
ARG DEBIAN_FRONTEND=noninteractive

# Deterministic UID (first user). Helps with docker build cache
ENV USER_ID=1000
# Delete the default ubuntu user & group UID=1000 GID=1000 in Ubuntu 23.04+
# that conflicts with the linuxbrew user
RUN touch /var/mail/ubuntu && chown ubuntu /var/mail/ubuntu && userdel -r ubuntu; true

# We don't want to manually pin versions, happy to use whatever
# Ubuntu thinks is best.
# hadolint ignore=DL3008

# We need `[` instead of `[[` because the shell is `/bin/sh`.
# shellcheck disable=SC1091,SC2154,SC2292
RUN true \
  && apt-get update \
  && apt-get install -y --no-install-recommends `# brew` \
    acl \
    bzip2 \
    ca-certificates \
    curl \
    file \
    fonts-dejavu-core \
    gcc \
    g++ \
    gawk \
    git \
    gpg \
    less \
    locales \
    make \
    netbase \
    openssh-client \
    patch \
    sudo \
    unzip \
    uuid-runtime \
    tzdata \
    jq \
  && apt-get install -y --no-install-recommends `# perl` \
    procps \
    cpio \
    libbz2-dev \
    libz-dev \
    zlib1g-dev \
    libdb-dev \
    libgdbm-dev \
    libssl-dev \
    libexpat1 \
  && apt-get install -y --no-install-recommends `# python` \
    sqlite3 \
    libsqlite3-dev \
    libbz2-dev \
    libssl-dev \
    libffi-dev \
  && apt-get autoremove --purge -y \
  && rm -rf /var/lib/apt/lists/* \
  && sed -i -E 's/^(USERGROUPS_ENAB\s+)yes$/\1no/' /etc/login.defs \
  && localedef -i en_US -f UTF-8 en_US.UTF-8 \
  && useradd -u "${USER_ID}" --create-home --shell /bin/bash --user-group linuxbrew \
  && echo 'linuxbrew ALL=(ALL) NOPASSWD:ALL' >>/etc/sudoers \
  && su - linuxbrew -c 'mkdir ~/.linuxbrew'

USER linuxbrew
COPY --chown=linuxbrew:linuxbrew . /home/linuxbrew/.linuxbrew/Homebrew
ENV PATH="/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:${PATH}" \
  XDG_CACHE_HOME=/home/linuxbrew/.cache
WORKDIR /home/linuxbrew

RUN --mount=type=cache,target=/home/linuxbrew/.cache,uid="${USER_ID}" \
   --mount=type=cache,target=/home/linuxbrew/.bundle,uid="${USER_ID}" \
   mkdir -p \
  .linuxbrew/bin \
  .linuxbrew/etc \
  .linuxbrew/include \
  .linuxbrew/lib \
  .linuxbrew/opt \
  .linuxbrew/sbin \
  .linuxbrew/share \
  .linuxbrew/var/homebrew/linked \
  .linuxbrew/Cellar \
  && ln -s ../Homebrew/bin/brew .linuxbrew/bin/brew \
  && curl -L https://github.com/Homebrew/brew/archive/refs/tags/4.4.10.tar.gz | tar xz --strip 1 -C .linuxbrew \
  && brew install-bundler-gems --groups=all \
  && brew cleanup \
  && { git -C .linuxbrew/Homebrew config --unset gc.auto; true; } \
  && { git -C .linuxbrew/Homebrew config --unset homebrew.devcmdrun; true; } \
  && touch .linuxbrew/.homebrewdocker

ENV PATH="/home/linuxbrew/Perl/bin:${PATH}"

RUN true \
    && mkdir -p /home/linuxbrew/Perl \
    && curl -L https://www.cpan.org/src/5.0/perl-5.34.3.tar.gz | tar xz \
    && cd perl-5.34.3 \
    && ./Configure \
        -des \
        -Dprefix=/home/linuxbrew/Perl \
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
