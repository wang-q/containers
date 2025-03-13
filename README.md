# Several docker containers

<!-- TOC -->
* [Several docker containers](#several-docker-containers)
  * [docker](#docker)
    * [base: perl and python](#base-perl-and-python)
    * [repeatmasker](#repeatmasker)
  * [singularity](#singularity)
    * [shims](#shims)
<!-- TOC -->

Containers were built with GitHub Actions and subsequently published to Docker Hub.

To run on HPC, use Singularity and create shims to run the containers

## docker

### base: perl and python

```shell
# Build
docker build -t wangq/base base/.

# Run
docker run --rm wangq/base:latest base help

docker run --rm -it wangq/base:master

```

### repeatmasker

```shell
# Build
docker build -t wangq/repeatmasker repeatmasker/.

# Run
docker run --rm wangq/repeatmasker:latest RepeatMasker

docker run --rm -it wangq/repeatmasker:master

```

## singularity

```shell
singularity pull docker://wangq/repeatmasker:master

singularity run repeatmasker_master.sif /app/RepeatMasker/RepeatMasker

singularity run repeatmasker_master.sif /app/RepeatMasker/util/rmOutToGFF3.pl

```

### vcpkg

Even with musl libc on Ubuntu 22.04, the generated tools are still linked to the system libc.
Therefore, CentOS 7 must be used as the base image.

```bash
mkdir -p $HOME/share/builds
cd $HOME/share/builds

singularity pull docker://wangq/vcpkg-centos:master

# rm -fr $HOME/.cache/vcpkg/archives/*

# glib -Wno-missing-prototypes -Wno-strict-prototypes
# fontconfig[tools] -std=gnu99
# pkgconf -D_GNU_SOURCE

singularity run --env CFLAGS="-D_GNU_SOURCE -std=gnu99 -Wno-missing-prototypes -Wno-strict-prototypes" \
vcpkg-centos_master.sif \
vcpkg install --debug --recurse \
    --clean-buildtrees-after-build --clean-packages-after-build \
    --x-buildtrees-root=./buildtrees \
    --downloads-root=./downloads \
    --x-install-root=./installed \
    --x-packages-root=./packages \
    graphviz:x64-linux-release

# cairo[core,fontconfig,freetype,gobject]

    # "curl[core,tool,ssl,http2,websockets]":x64-linux-release

    # fontconfig[tools]:x64-linux-release

ldd -v installed/x64-linux-musl/tools/fontconfig/fc-cache

singularity run vcpkg-centos_master.sif \
vcpkg install --debug --recurse --allow-unsupported \
    --clean-buildtrees-after-build --clean-packages-after-build \
    --x-buildtrees-root=./buildtrees \
    --downloads-root=./downloads \
    --x-install-root=./installed \
    --x-packages-root=./packages \
    graphviz:x64-linux-musl

singularity run vcpkg-centos_master.sif ldd -v installed/x64-linux-musl/tools/bzip2/bzip2
ldd -v installed/x64-linux-musl/tools/bzip2/bzip2

vcpkg install --debug --recurse \
    --x-buildtrees-root=./buildtrees \
    --downloads-root=./downloads \
    --x-install-root=./installed \
    --x-packages-root=./packages \
    vcpkg-tool-meson:x64-linux vcpkg-tool-meson:x64-linux-release

```


### shims

```shell
mv repeatmasker_master.sif ~/bin/

# RepeatMasker
cat << EOF > ~/bin/RepeatMasker
#!/usr/bin/env bash
singularity run ~/bin/repeatmasker_master.sif /app/RepeatMasker/RepeatMasker $@
EOF
chmod +x ~/bin/RepeatMasker

# rmOutToGFF3
cat << EOF > ~/bin/rmOutToGFF3
#!/usr/bin/env bash
singularity run ~/bin/repeatmasker_master.sif /app/RepeatMasker/util/rmOutToGFF3.pl $@
EOF
chmod +x ~/bin/rmOutToGFF3

RepeatMasker
rmOutToGFF3

```
