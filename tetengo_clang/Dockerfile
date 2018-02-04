# Dockerfile for tetengo/clang
# Copyright (C) 2017 kaoru

FROM tetengo/base

LABEL maintainer kaoru http://twitter.com/kaorut

#------------------------------------------------------------------------------

RUN \
  apt-get -y install \
    clang \
    clang-3.9 \
    iwyu

#------------------------------------------------------------------------------

RUN \
  apt-get -y install \
    libbz2-dev \
    libpython-dev

ARG BOOST_VER=1_66_0
ARG BOOST_VER_DOT=1.66.0
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
  apt-get -y install \
    cmake \
    graphviz

ARG DOXYGEN_VER=1.8.14
WORKDIR /root
RUN \
  wget http://ftp.stack.nl/pub/users/dimitri/doxygen-${DOXYGEN_VER}.src.tar.gz && \
  tar axvf doxygen-${DOXYGEN_VER}.src.tar.gz && \
  mkdir /root/doxygen-${DOXYGEN_VER}/build
WORKDIR /root/doxygen-${DOXYGEN_VER}/build
RUN \
  cmake -G "Unix Makefiles" .. && \
  make -j8 install

#------------------------------------------------------------------------------

RUN \
  useradd -g users -G sudo -m docker && \
  echo "docker:docker" | chpasswd && \
  echo "export LANG=ja_JP.UTF-8" >> /home/docker/.bashrc && \
  echo "export GIT_EDITOR=emacs" >> /home/docker/.bashrc

WORKDIR /home/docker
ENTRYPOINT /bin/bash
