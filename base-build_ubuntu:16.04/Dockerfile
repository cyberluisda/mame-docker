##
# Example to build
#
# docker build --tag mame-base-build:16.04 .
FROM ubuntu:16.04

LABEL maintainer="Luis David Barrios <cyberluisda@gmail.com>"

###
# This section can be considered build base
###

# Paths
RUN mkdir -p roms /build /opt/tmp

# Get current list of installed packages
RUN dpkg --get-selections | fgrep -v deinstall | sort > /opt/tmp/pkg_installed

# Install build tools (FIXME: to one RUN when dev finished)
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        gconf2 \
        libgconf2-dev \
    	pkg-config \
    	libgtk2.0-dev \
        libqt4-dev \
    	libsdl2-dev \
        libsdl2-ttf-dev \
        coreutils \
        unzip \
        curl



