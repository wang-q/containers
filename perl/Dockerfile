FROM wangq/brew
LABEL maintainer="Qiang Wang <wang-q@outlook.com>"

# Perl
RUN true \
  && export HOMEBREW_NO_ANALYTICS=1 \
  && export HOMEBREW_NO_AUTO_UPDATE=1 \
  && brew install perl \
  && curl -L https://cpanmin.us | perl - App::cpanminus \
  && brew cleanup \
  && rm -fr $(brew --cache)/* \
  && rm -fr $HOME/.cpan \
  && rm -fr $HOME/.gem \
  && rm -fr $HOME/.cpanm

# Change this when Perl updated
ENV PATH=/home/linuxbrew/bin:/home/linuxbrew/.linuxbrew/Cellar/perl/5.40.0/bin:$PATH

WORKDIR /home/linuxbrew
ADD . .
