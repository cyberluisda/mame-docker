##
# Example to build
#
# docker build --tag mame:0.161 .
##
# Example to run
#
# docker run --rm -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix  -v /YOUR_LOCAL_ROOMS_PATH:/roms mame:0.161
##
# If you have X11 display errors like:
#
# `Could not initialize SDL Failed to connect to the Mir Server`
#
# Run `xhost +` in your host to enable acces to X11 from other than localhost.
##
FROM ubuntu:16.04

ENV MAME_VERSION=0161

# Paths
RUN mkdir -p /roms /build /opt/tmp /mame

## Same steps like ../base-build_ubuntu:XX.XX and ./Dockerfile-dev, and remove
# dev packages. But in only one RUN to prevent heavy size of image
RUN dpkg --get-selections | fgrep -v deinstall | sort > /opt/tmp/pkg_installed \
  && apt-get update \
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
    curl \
  && curl \
    -ksL \
    -o /tmp/mame${MAME_VERSION}s.zip \
    https://github.com/mamedev/mame/releases/download/mame${MAME_VERSION}/mame${MAME_VERSION}s.zip \
  && unzip /tmp/mame${MAME_VERSION}s.zip -d /tmp \
  && unzip /tmp/mame.zip -d /build \
  && rm -f /tmp/mame${MAME_VERSION}s.zip /tmp/mame.zip \
  && cd /build \
  && make \
    NOWERROR=1 \
    TOOLS=1 \
    -j5 \
  && mkdir -p /opt/mame \
  && find /build -maxdepth 1 -perm -111 -type f -exec cp -v {} /opt/mame \; \
  && rm -fr /build \
  && dpkg --get-selections \
    | fgrep -v deinstall | sort > /opt/tmp/pkg_new \
  && comm -2 -3 /opt/tmp/pkg_new /opt/tmp/pkg_installed \
    | cut -f 1 \
    | xargs apt-get -y --allow-remove-essential purge \
  && apt-get -y --allow-remove-essential clean \
  && apt-get install -y --no-install-recommends \
    libsdl2-2.0-0 \
    libgl1-mesa-glx \
    libqtgui4 \
    libsdl2-ttf-2.0-0 \
  && rm -rf \
   /var/lib/apt/lists/* \
   /opt/tmp

CMD [ "/opt/mame/mame64", "-rp", "/roms" ]
WORKDIR /mame
