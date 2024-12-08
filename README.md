# Several docker containers

## base: perl and python

```shell
# Build
docker build -t wangq/base base/.

# Run
docker run --rm wangq/base:latest base help

docker run --rm -it wangq/base:master

```

## repeatmasker

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
