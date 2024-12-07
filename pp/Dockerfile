FROM wangq/brew:master
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

# Perl & Python
RUN true \
  && export HOMEBREW_NO_ANALYTICS=1 \
  && export HOMEBREW_NO_AUTO_UPDATE=1 \
  && brew install perl \
  && curl -L https://cpanmin.us | perl - App::cpanminus \
  && brew install python \
  && brew cleanup \
  && rm -fr $(brew --cache)/* \
  && rm -fr $HOME/.cpan \
  && rm -fr $HOME/.cpanm \
  && rm -fr $HOME/.gem

# Change this when Perl updated
ENV PATH=/home/linuxbrew/bin:/home/linuxbrew/.linuxbrew/Cellar/perl/5.40.0/bin:$PATH

# Modules
# Text::Soundex and h5py are needed by RepeatMasker 4.1.1
RUN true \
  && export HOMEBREW_NO_ANALYTICS=1 \
  && export HOMEBREW_NO_AUTO_UPDATE=1 \
  && cpanm -nq Text::Soundex \
  && pip3 install h5py --break-system-packages \
  && rm -fr $HOME/.cpan \
  && rm -fr $HOME/.cpanm \
  && rm -fr $HOME/.gem

WORKDIR /home/linuxbrew
ADD . .
