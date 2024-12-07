# Several docker containers

## perl

```powershell
# Build
docker build -t wangq/perl perl/.

# Run
docker run --rm wangq/perl:latest perl -V

docker run --rm -it wangq/perl

```

## repeatmasker

```powershell
# Build
docker build -t wangq/repeatmasker repeatmasker/.

# Run
docker run --rm wangq/repeatmasker:latest RepeatMasker

docker run --rm -it wangq/repeatmasker:latest

```
