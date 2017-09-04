FROM lsiobase/xenial.arm64
MAINTAINER Stian Larsen, sparklyballs

# set version label
ARG BUILD_DATE
ARG VERSION
LABEL build_version="Linuxserver.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"

# global environment settings
ENV DEBIAN_FRONTEND="noninteractive" \
PLEX_DOWNLOAD="https://downloads.plex.tv/plex-media-server" \
PLEX_INSTALL="https://plex.tv/downloads/latest/1?channel=8&build=linux-ubuntu-x86_64&distro=ubuntu" \
PLEX_MEDIA_SERVER_APPLICATION_SUPPORT_DIR="/config/Library/Application Support" \
PLEX_MEDIA_SERVER_HOME="/usr/lib/plexmediaserver" \
PLEX_MEDIA_SERVER_INFO_DEVICE=docker \
PLEX_MEDIA_SERVER_MAX_PLUGIN_PROCS="6" \
PLEX_MEDIA_SERVER_USER=abc

# install packages
RUN \
 apt-get update && \
 apt-get install -y \
	avahi-daemon \
	dbus \
	wget \
  apt-transport-https && \

# install plex
 wget -4 -O - https://dev2day.de/pms/dev2day-pms.gpg.key | apt-key add - && \
 echo "deb [arch=armhf] https://dev2day.de/pms/ jessie main" >> /etc/apt/sources.list.d/pms.list && \
 dpkg --add-architecture armhf && \
 apt-get update && apt-get install -y libstdc++6:armhf && \

 apt-get update && \
 apt-get install -y \
 plexmediaserver-installer:armhf && \

# change abc home folder to fix plex hanging at runtime with usermod
 usermod -d /app abc && \

# cleanup
 apt-get clean && \
 rm -rf \
	/etc/default/plexmediaserver \
	/tmp/* \
	/var/lib/apt/lists/* \
	/var/tmp/*

# add local files
COPY root/ /

# ports and volumes
EXPOSE 32400 32400/udp 32469 32469/udp 5353/udp 1900/udp
VOLUME /config /transcode
