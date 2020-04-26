##
# Example to build
#
# docker build --tag mame-base-build:18.04 .
##
FROM ubuntu:18.04

LABEL maintainer="Luis David Barrios <cyberluisda@gmail.com>"

###
# This section can be considered build base
###

# Paths
RUN mkdir -p /roms /build /opt/tmp /mame

# Get current list of installed packages
RUN dpkg --get-selections | fgrep -v deinstall | sort > /opt/tmp/pkg_installed

# Install build tools (FIXME: to one RUN when dev finished)
# ruby, ruby-dev and rubygems only required for fpm
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
      build-essential \
      python \
    	libfontconfig-dev \
      qt5-default \
    	libsdl2-dev \
      libsdl2-ttf-dev \
      coreutils \
      unzip \
      curl \
      ruby \
      ruby-dev \
      rubygems
# Install fpm only for package
RUN gem install --no-document fpm
ENV PKG_CONFIG_PATH /usr/lib/x86_64-linux-gnu/pkgconfig/:$PKG_CONFIG_PATH
