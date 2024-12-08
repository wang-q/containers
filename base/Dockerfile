FROM ubuntu:22.04
ARG DEBIAN_FRONTEND=noninteractive

# Delete the default ubuntu user & group UID=1000 GID=1000 in Ubuntu 23.04+
RUN touch /var/mail/ubuntu && chown ubuntu /var/mail/ubuntu && userdel -r ubuntu; true

#https://docs.sylabs.io/guides/3.2/user-guide/definition_files.html?highlight=best%20practice#best-practices-for-build-recipes \

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
  && apt-get install -y --no-install-recommends perl cpanminus python3 python3-pip python3-pip-whl \
  && apt-get autoremove --purge -y \
  && rm -rf /var/lib/apt/lists/* \
  && localedef -i en_US -f UTF-8 en_US.UTF-8 \
  && mkdir -p app

WORKDIR /app

RUN true \
    && cpanm -nq Text::Soundex

RUN true \
    && pip3 install h5py
