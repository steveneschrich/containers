FROM ubuntu:20.04

LABEL maintainer="Steven.Eschrich@moffitt.org"
LABEL version="0.1"
LABEL description="Affymetrix Analysis Power Tools"

# Disable Prompt During Packages Installation
ARG DEBIAN_FRONTEND=noninteractive  

COPY apt_2.11.4_linux_64_bit_x86_binaries.zip /tmp

# Update Ubuntu Software repository
RUN apt update && \
    apt install -y wget ca-certificates locales &&  \

    wget --no-check-certificate -O /usr/local/share/ca-certificates/moffitt-ca-int.crt \
                        "https://gitlab.moffitt.usf.edu:8000/singularity/mcc-certificates/-/raw/main/certs/moffitt-ca-int.cer" && \

    wget --no-check-certificate -O /usr/local/share/ca-certificates/moffitt-ca.crt \
                        "https://gitlab.moffitt.usf.edu:8000/singularity/mcc-certificates/-/raw/main/certs/moffitt-ca.cer"  && \
	wget --no-check-certificate -O /usr/local/share/ca-certificates/moffitt-chain \
                        "https://gitlab.moffitt.usf.edu:8000/singularity/mcc-certificates/-/raw/main/certs/moffitt-chain" && \
    chmod 644 /usr/local/share/ca-certificates/moffitt* && \
	# Given the new certificates in /usr/share/ca-certificates,
	# dkpg-reconfigure regenerates the /etc/ca-certificates.conf to
	# pick them up. Then, run update-ca-certificates to install in
	# /etc/ssl. This seems a bit round-about.
	#dpkg-reconfigure ca-certificates
	update-ca-certificates --verbose && \
	echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen en_US.utf8 && update-locale LANG=en_US.UTF-8

RUN cd /tmp && \
    apt install unzip && \
    unzip /tmp/apt_2.11.4_linux_64_bit_x86_binaries.zip && \
    chmod 755 /tmp/apt_2.11.4_linux_64_bit_x86_binaries/bin/* && \
    mv /tmp/apt_2.11.4_linux_64_bit_x86_binaries/bin/* /usr/bin && \
    mkdir -p /usr/bin/doc && \
    mv /tmp/apt_2.11.4_linux_64_bit_x86_binaries/doc/* /usr/bin/doc && \
    rm -rf /tmp/apt_2.11.4_linux_64_bit_x86_binaries
	



ENV LC_ALL=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV TZ=America/New_York
ENV PATH=${PATH}:/usr/bin

