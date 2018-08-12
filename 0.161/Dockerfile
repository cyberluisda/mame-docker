##
# Require base version build from ../base-build:16.04 
##
# Example to build
#
# docer build --tag mame:0.161 .
##
# Example to run
# 
# docker run --rm -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix  -v /YOUR_LOCAL_ROOMS_PATH:/roms mame:0.161 -rp /roms
## 
# If you have X11 display errors like:
# 
# `Could not initialize SDL Failed to connect to the Mir Server`
#
# Run `xhost +` in your host to enable acces to X11 from other than localhost.
##

FROM mame-base-build:16.04

ENV MAME_VERSION=0161

# Download mame source code
RUN curl \
        -ksL \
        -o /tmp/mame${MAME_VERSION}s.zip \
        https://github.com/mamedev/mame/releases/download/mame${MAME_VERSION}/mame${MAME_VERSION}s.zip \
    && unzip /tmp/mame${MAME_VERSION}s.zip -d /tmp \
    && unzip /tmp/mame.zip -d /build \
    && rm -f /tmp/mame${MAME_VERSION}s.zip /tmp/mame.zip


# Build and install
# TODO mix in one command only when debug was finished
RUN cd /build \
    && make
RUN make install \
    && cd 

# Clean
# TODO uncomment when debug was finished
# RUN rm -fr /build

# Remove build packages
RUN dpkg --get-selections \ 
        | fgrep -v deinstall > /opt/tmp/pkg_new \
    && comm -3 /opt/tmp/pkg_new /opt/tmp/pkg_installed \
        | cut -f 1 \
        | xargs apt-get purge \
    && apt-get clean \
    && rm -rf \
       /var/lib/apt/lists/* \
       /opt/tmp

ENTRYPOINT /usr/game/mame
WORKDIR /roms

