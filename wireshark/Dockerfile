FROM ubuntu:20.04
LABEL maintainer "Martin Buchleitner <mabunixda@gmail.com>"

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
	&& apt-get install -y software-properties-common --no-install-recommends && \
	add-apt-repository ppa:wireshark-dev/stable && \
	apt-get update && \
	apt-get install -y \
	wireshark \
	&& rm -rf /var/lib/apt/lists/*

ENV HOME /home/app
RUN useradd --create-home --uid 1000 --home-dir $HOME app \
	&& chown -R app:app $HOME

RUN chown root:app /usr/bin/dumpcap \
	&& setcap 'CAP_NET_RAW+eip CAP_NET_ADMIN+eip' /usr/bin/dumpcap

USER app

WORKDIR $HOME

ENTRYPOINT	[ "wireshark" ]
