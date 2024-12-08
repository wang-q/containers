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
