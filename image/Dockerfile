ARG UBUNTU_VERSION=latest

FROM ubuntu:${UBUNTU_VERSION}
LABEL maintainer="dekart811" \
	com.steamcmd.description="Ubuntu based image for SteamCMD."

ARG USER_ID=1000
ARG GROUP_ID=1000

ENV DEBIAN_FRONTEND noninteractive
ENV STEAM_ARGS ""

RUN apt-get update &&\
	apt-get upgrade -y &&\
	apt-get install -y locales &&\
	localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

ENV LANG en_US.utf8

RUN apt-get install -y curl lib32gcc1 &&\
	apt-get autoremove -y &&\
	apt-get clean &&\
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN groupadd -g ${GROUP_ID} steamcmd &&\
	useradd -m -d "/steam" -g ${GROUP_ID} -u ${USER_ID} steamcmd

USER steamcmd
WORKDIR /steam

RUN mkdir -p Steam &&\
	cd Steam &&\
	curl -sqL https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz | tar zxvf - &&\
	rm -f steamcmd_linux.tar.gz

WORKDIR /steam/Steam

COPY ./init.sh /steam/Steam/init.sh

VOLUME ["/steam"]

CMD ["/bin/bash","/steam/Steam/init.sh"]
