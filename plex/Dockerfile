FROM arm64v8/debian:jessie
MAINTAINER Drew Worthey


# global environment settings
ENV DEBIAN_FRONTEND="noninteractive"

# install packages
RUN \
 apt-get update && \
 apt-get install -y wget && \

# install plex
 wget -O - https://dev2day.de/pms/dev2day-pms.gpg.key | apt-key add - && \
 echo "deb [arch=armhf] https://dev2day.de/pms/ jessie main" >> /etc/apt/sources.list.d/pms.list && \
 apt-get install -y apt-transport-https && \
 dpkg --add-architecture armhf && \
 wget http://archive.raspbian.org/raspbian/pool/main/g/gcc-4.9/libstdc++6_4.9.2-10_armhf.deb && \
 dpkg -i libstdc++6_4.9.2-10_armhf.deb && \
 rm libstdc++6_4.9.2-10_armhf.deb && \
 apt-get clean

ENV \
 PLEX_MEDIA_SERVER_APPLICATION_SUPPORT_DIR="/config/Library/Application Support" \
 PLEX_MEDIA_SERVER_HOME="/usr/lib/plexmediaserver" \
 PLEX_MEDIA_SERVER_INFO_DEVICE=docker \
 PLEX_MEDIA_SERVER_MAX_PLUGIN_PROCS="6" \
 PLEX_MEDIA_SERVER_USER=root


RUN apt-get update && \
 apt-get install -y \
  plexmediaserver-installer:armhf && \

# change abc home folder to fix plex hanging at runtime with usermod
# usermod -d /app root && \

# cleanup
 apt-get clean && \
 rm -rf \
	/etc/default/plexmediaserver \
	/tmp/* \
	/var/lib/apt/lists/* \
	/var/tmp/*

# add local files
# COPY root/ /

# ports and volumes
EXPOSE 32400 32400/udp 32469 32469/udp 5353/udp 1900/udp
VOLUME /config /transcode
