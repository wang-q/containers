ARG version=22.04
# version is passed through by Docker.
# shellcheck disable=SC2154
FROM ubuntu:"${version}"
ARG DEBIAN_FRONTEND=noninteractive

# Delete the default ubuntu user & group UID=1000 GID=1000 in Ubuntu 23.04+
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
    xz-utils \
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
  && localedef -i en_US -f UTF-8 en_US.UTF-8

ENV PATH="/root/homebrew/bin:/root/homebrew/sbin:${PATH}"

RUN true \
  && mkdir -p homebrew \
  && ln -s ../Homebrew/bin/brew homebrew/bin/brew \
  && curl -L https://github.com/Homebrew/brew/archive/refs/tags/4.4.10.tar.gz | tar xz --strip 1 -C homebrew \
  && brew install-bundler-gems --groups=all \
  && brew cleanup \
  && rm -rf $(brew --cache) \
