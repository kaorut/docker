# Dockerfile for tetengo/base
# Copyright (C) 2017 kaoru

FROM debian:jessie

LABEL maintainer kaoru http://twitter.com/kaorut

#------------------------------------------------------------------------------

RUN \
  apt-get -y update && \
  apt-get -y upgrade && \
  apt-get -y install \
    autoconf \
    autoconf-archive \
    automake \
    bison \
    bzip2 \
    cmake \
    ctags \
    emacs \
    flex \
    g++ \
    g++-4.9 \
    git \
    graphviz \
    less \
    libbz2-dev \
    libpython-dev \
    locales-all \
    make \
    python \
    sudo \
    unzip \
    wget \
    zip

#------------------------------------------------------------------------------

ARG BOOST_VER=1_63_0
ARG BOOST_VER_DOT=1.63.0
WORKDIR /root
RUN \
  wget https://downloads.sourceforge.net/project/boost/boost/${BOOST_VER_DOT}/boost_${BOOST_VER}.tar.bz2 && \
  tar axvf boost_${BOOST_VER}.tar.bz2
WORKDIR /root/boost_${BOOST_VER}
RUN \
  ./bootstrap.sh && \
  ./b2 -j8 toolset=gcc link=static cxxflags="-std=gnu++11" install --prefix=/usr/local

#------------------------------------------------------------------------------

ARG DOXYGEN_VER=1.8.13
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
  echo "export LANG=ja_JP.UTF-8" >> /home/docker/.bashrc

#------------------------------------------------------------------------------

WORKDIR /home/docker
ENTRYPOINT /bin/bash
