FROM wangq/brewpp:master
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

# RepeatMasker
# https://stackoverflow.com/questions/57629010/linuxbrew-curl-certificate-issue
RUN true \
  && export HOMEBREW_NO_ANALYTICS=1 \
  && export HOMEBREW_NO_AUTO_UPDATE=1 \
  && export HOMEBREW_CURLRC=1 \
  && echo "--ciphers DEFAULT@SECLEVEL=1" >> $HOME/.curlrc \
  && brew install hmmer \
  && brew install wang-q/tap/rmblast@2.14.1 \
  && brew install wang-q/tap/trf@4 \
  && brew install wang-q/tap/repeatmasker@4.1.1 \
  && cd $(brew --prefix)/Cellar/repeatmasker@4.1.1/4.1.1/libexec \
  && perl configure \
        -hmmer_dir=$(brew --prefix)/bin \
        -rmblast_dir=$(brew --prefix)/bin \
        -libdir=$(brew --prefix)/Cellar/repeatmasker@4.1.1/4.1.1/libexec/Libraries \
        -trf_prgm=$(brew --prefix)/bin/trf \
        -default_search_engine=rmblast \
  && rm -fr $(brew --cache)/* \
  && rm -fr $(brew --prefix)/Homebrew/Library/Taps/*

WORKDIR /home/linuxbrew
ADD . .
