# Dockerfile for tetengo/clang
# Copyright (C) 2017 kaoru

FROM tetengo/base

LABEL maintainer kaoru http://twitter.com/kaorut

#------------------------------------------------------------------------------

RUN \
  apt-get -y install \
    clang \
    clang-3.5

#------------------------------------------------------------------------------

RUN \
  apt-get -y install \
    libbz2-dev \
    libpython-dev

ARG BOOST_VER=1_63_0
ARG BOOST_VER_DOT=1.63.0
WORKDIR /root
RUN \
  wget https://downloads.sourceforge.net/project/boost/boost/${BOOST_VER_DOT}/boost_${BOOST_VER}.tar.bz2 && \
  tar axvf boost_${BOOST_VER}.tar.bz2
WORKDIR /root/boost_${BOOST_VER}
RUN \
  ./bootstrap.sh --with-toolset=clang && \
  ./b2 -j8 toolset=clang link=static cxxflags="-std=gnu++11" install --prefix=/usr/local

#------------------------------------------------------------------------------

RUN \
  useradd -g users -G sudo -m docker && \
  echo "docker:docker" | chpasswd && \
  echo "export LANG=ja_JP.UTF-8" >> /home/docker/.bashrc && \
  echo "export GIT_EDITOR=emacs" >> /home/docker/.bashrc

WORKDIR /home/docker
ENTRYPOINT /bin/bash
