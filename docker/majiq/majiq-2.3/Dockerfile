FROM ubuntu:20.04

LABEL maintainer="Steven.Eschrich@moffitt.org"
LABEL version="0.1"
LABEL description="This is a majiq image with basic tools."

# Disable Prompt During Packages Installation
ARG DEBIAN_FRONTEND=noninteractive  
ARG MAJIQ_URL

# Update Ubuntu Software repository
RUN apt update && \
    apt install -y wget ca-certificates locales &&  \
    wget --no-check-certificate -O /usr/local/share/ca-certificates/moffitt-ca.crt \
                        "https://gitlab.moffitt.usf.edu:8000/singularity/mcc-certificates/-/blob/main/certs/moffitt-ca.cer"  && \
    wget --no-check-certificate -O /usr/local/share/ca-certificates/moffitt-ca-int.crt \
                        "https://gitlab.moffitt.usf.edu:8000/singularity/mcc-certificates/-/blob/main/certs/moffitt-ca-int.cer" && \
	wget --no-check-certificate -O /usr/local/share/ca-certificates/moffitt-chain \
                        "https://gitlab.moffitt.usf.edu:8000/singularity/mcc-certificates/-/blob/main/certs/moffitt-chain" && \
                        chmod 644 /usr/local/share/ca-certificates/moffitt* && \
	# Given the new certificates in /usr/share/ca-certificates,
	# dkpg-reconfigure regenerates the /etc/ca-certificates.conf to
	# pick them up. Then, run update-ca-certificates to install in
	# /etc/ssl. This seems a bit round-about.
	#dpkg-reconfigure ca-certificates
	update-ca-certificates --verbose && \
	echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen en_US.utf8 && update-locale LANG=en_US.UTF-8

RUN apt-get install -y apt-transport-https software-properties-common && \
    apt-get -y -qq install  \
	python3 \
	python3-venv \
	python3-pip \
	gcc \
	make \
	git \
	libbz2-dev \
	zlib1g-dev \
	libncurses5-dev \
	libncursesw5-dev \
	liblzma-dev  \
        libssl-dev \
	libcurl4 \
	libcurl4-openssl-dev  \
	libhts-dev
	
RUN git clone --config http.sslVerify=false -q $MAJIQ_URL /tmp/majiq_git && \
   pip3 install /tmp/majiq_git && \
   rm -rf /tmp/majiq_git

ENV LC_ALL=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV TZ=America/New_York
