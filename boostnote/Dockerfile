# DESCRIPTION:  Create the boostnote app on a container
# AUTHOR:       Matheus Paiva <matheus.a.paiva@gmail.com>
# COMMENTS:
#       This file describes how to build the boostnote app in a container with all dependencies
#       installed.
# USAGE:
#       Build:
#       `docker build -t boostnote .`
#
#       Run:
#       `docker run -ti --name=boostnote -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix boostnote boostnote`
#
#       Troubleshooting
#
#       Probably you'll need to grant your user access to the X server. You can do so using `xhost`:
#       `xhost +SI:localuser:$(id -un)`

# Base docker image
FROM debian:stretch
LABEL maintainer "Matheus Paiva <matheus.a.paiva@gmail.com>"

# Install dependencies
RUN apt-get update && apt-get install -y \
	git \
	gconf2 \
	gconf-service \
	gvfs-bin \
	libasound2 \
	libcap2 \
	libgconf-2-4 \
	libgnome-keyring-dev \
	libgtk2.0-0 \
	libnotify4 \
	libnss3 \
	libxkbfile1 \
	libxss1 \
	libxtst6 \
	libx11-xcb-dev \
  libcanberra-gtk-module \
	xdg-utils \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENV BOOSTNOTE_VERSION 0.8.16

# download the source
RUN buildDeps=' \
		ca-certificates \
		curl \
	' \
	&& set -x \
	&& apt-get update && apt-get install -y $buildDeps --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/* \
  && curl -sSL https://github.com/BoostIO/boost-releases/releases/download/v${BOOSTNOTE_VERSION}/boostnote_${BOOSTNOTE_VERSION}_amd64.deb -o /tmp/boostnote-amd64.deb \
	&& dpkg -i /tmp/boostnote-amd64.deb \
	&& rm -rf /tmp/*.deb \
	&& apt-get purge -y --auto-remove $buildDeps


# Autorun boostnote
ENTRYPOINT [ "boostnote"]
