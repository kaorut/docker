# Dockerfile for tetengo/clang
# Copyright (C) 2017-2019 kaoru

FROM tetengo/base

LABEL maintainer kaoru http://twitter.com/kaorut

#------------------------------------------------------------------------------

RUN \
  apt-get -y update && \
  apt-get -y install \
    clang \
    clang-7

#------------------------------------------------------------------------------

RUN \
  apt-get -y update && \
  apt-get -y install \
    libbz2-dev \
    libpython-dev

ARG BOOST_VER=1_71_0
ARG BOOST_VER_DOT=1.71.0
WORKDIR /root
RUN \
  wget https://dl.bintray.com/boostorg/release/${BOOST_VER_DOT}/source/boost_${BOOST_VER}.tar.bz2 && \
  tar axvf boost_${BOOST_VER}.tar.bz2
WORKDIR /root/boost_${BOOST_VER}
RUN \
  ./bootstrap.sh --with-toolset=clang && \
  (./b2 -j8 toolset=clang link=static cxxflags="-std=gnu++11" install --prefix=/usr/local || :)

#------------------------------------------------------------------------------

RUN \
  useradd -g users -G sudo -m docker && \
  echo "docker:docker" | chpasswd && \
  echo "export LANG=ja_JP.UTF-8" >> /home/docker/.bashrc && \
  echo "export GIT_EDITOR=emacs" >> /home/docker/.bashrc

WORKDIR /home/docker
ENTRYPOINT /bin/bash
