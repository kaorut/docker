# Dockerfile for tetengo/base
# Copyright (C) 2017 kaoru

FROM debian:stretch

LABEL maintainer kaoru http://twitter.com/kaorut

#------------------------------------------------------------------------------

RUN \
  apt-get -y update && \
  apt-get -y upgrade

#------------------------------------------------------------------------------

RUN \
  apt-get -y install \
    bzip2 \
    curl \
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
  apt-get -y install \
    autoconf \
    autoconf-archive \
    automake \
    bison \
    ctags \
    flex \
    gdb \
    make

