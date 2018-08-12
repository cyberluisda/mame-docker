# Based on https://github.com/pataquets/docker-mame
# But set ubuntu base version to fix mame version
##
# Example to build
#
# docer build --tag magme:0.160 .
##
# Example to run
# 
# docker run --rm -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix  -v /YOUR_LOCAL_ROOMS_PATH:/roms mame:0.160 -rp /roms
## 
# If you have X11 display errors like:
# 
# `Could not initialize SDL Failed to connect to the Mir Server`
#
# Run `xhost +` in your host to enable acces to X11 from other than localhost.
##

FROM ubuntu:16.04

LABEL maintainer="Luis David Barrios <cyberluisda@gmail.com>"


RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \
	libgl1-mesa-glx \
        mame \
	mesa-utils \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*


ENTRYPOINT /usr/game/mame

###
# docker run --rm -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix  -v $PWD:/roms --entrypoint /bin/bash mame:0.160
# SKIP=yes; ls -1 | sort | while read -r fil; do name=$(basename $fil .zip); if [ "$SKIP" == "yes" ]; then echo "Skipping $name"; else echo "==== $fil"; /usr/games/mame -rp $PWD -nothrottle -speed 2 $name; fi; if [ "$fil" == "skullxbo1.zip" ]; then SKIP="no"; fi; done

