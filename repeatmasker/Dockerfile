FROM homebrew/brew
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

# Perl
RUN true \
 && export HOMEBREW_NO_ANALYTICS=1 \
 && export HOMEBREW_NO_AUTO_UPDATE=1 \
 && brew install perl \
 && curl -L https://cpanmin.us | perl - App::cpanminus \
 && rm -fr $(brew --cache)/* \
 && rm -fr $HOME/.cpan \
 && rm -fr $HOME/.gem \
 && rm -fr $HOME/.cpanm

# Change this when Perl updated
ENV PATH=/home/linuxbrew/bin:/home/linuxbrew/.linuxbrew/Cellar/perl/5.40.0/bin:$PATH

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
 && rm -fr $(brew --cache)/*

# brew untap
RUN true \
 && export HOMEBREW_NO_ANALYTICS=1 \
 && export HOMEBREW_NO_AUTO_UPDATE=1 \
 && brew untap --force homebrew/homebrew-core \
 && brew untap --force wang-q/tap

WORKDIR /home/linuxbrew
ADD . .
