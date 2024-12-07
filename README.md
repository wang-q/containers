# Several docker containers

## brew

```powershell
# Build
docker build -t wangq/brew brew/.

# Run
docker run --rm wangq/brew:latest brew help

docker run --rm -it wangq/brew

```

## perl and python

```powershell
# Build
docker build -t wangq/brewpp brewpp/.

# Run
docker run --rm wangq/brewpp:latest perl -V

docker run --rm -it wangq/brewpp:master

```

## repeatmasker

```powershell
# Build
docker build -t wangq/repeatmasker repeatmasker/.

# Run
docker run --rm wangq/repeatmasker:latest RepeatMasker

docker run --rm -it wangq/repeatmasker:latest

```
