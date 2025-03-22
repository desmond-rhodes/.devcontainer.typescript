FROM debian:bookworm

RUN \
	apt-get update && \
	apt-get -y dist-upgrade && \
	apt-get -y autopurge && \
	apt-get -y install \
		curl \
		locales \
	&& \
	sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen && \
	locale-gen && \
	useradd devcontainer --shell /bin/bash --create-home

ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8

USER devcontainer
WORKDIR /home/devcontainer

RUN \
	export NODE_VERSION='node' && \
	curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash && \
	mkdir example && \
	cd example && \
	bash -c " \
		. $HOME/.nvm/nvm.sh && \
		npm install npm --save-dev && \
		npx npm install typescript --save-dev \
	"

USER root
RUN apt-get -y install \
	man \
	less \
	vim \
	git
USER devcontainer
