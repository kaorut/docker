# Dockerfile for tetengo/base
# Copyright (C) 2017-2019 kaoru

FROM debian:buster

LABEL maintainer kaoru http://twitter.com/kaorut

#------------------------------------------------------------------------------

RUN \
  echo "deb http://ftp.jp.debian.org/debian/ buster-backports main" >> /etc/apt/sources.list

RUN \
  apt-get -y update && \
  apt-get -y upgrade

#------------------------------------------------------------------------------

RUN \
  apt-get -y update && \
  apt-get -y install \
    bzip2 \
    curl \
    dos2unix \
    emacs \
    git \
    less \
    locales-all \
    man \
    python \
    sudo \
    unzip \
    wget \
    zip

#------------------------------------------------------------------------------

RUN \
  apt-get -y update && \
  apt-get -y install \
    autoconf \
    autoconf-archive \
    automake \
    bison \
    clang \
    clang-7 \
    clang-format \
    clang-format-7 \
    ctags \
    flex \
    g++ \
    gdb \
    iwyu \
    libtool \
    make

#------------------------------------------------------------------------------

RUN \
  apt-get -y update && \
  apt-get -y install \
    cmake \
    graphviz

ARG DOXYGEN_VER=1.8.16
WORKDIR /root
RUN \
  wget http://doxygen.nl/files/doxygen-${DOXYGEN_VER}.src.tar.gz && \
  tar axvf doxygen-${DOXYGEN_VER}.src.tar.gz && \
  mkdir /root/doxygen-${DOXYGEN_VER}/build
WORKDIR /root/doxygen-${DOXYGEN_VER}/build
RUN \
  cmake -G "Unix Makefiles" .. && \
  make -j8 install

