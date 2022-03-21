FROM ubuntu:20.04

LABEL maintainer="Steven.Eschrich@moffitt.org"
LABEL version="0.1"
LABEL description="This is a base Ubuntu 20.04 image with basic tools."

# Disable Prompt During Packages Installation
ARG DEBIAN_FRONTEND=noninteractive  

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

RUN apt-get update && \
	apt-get install -y apt-transport-https software-properties-common && \
	apt-get -y -qq install  \
	lmod \
	proj-bin \
	libproj-dev \
        libcairo2-dev \
        libx11-dev \
        libxt-dev \
        perl \
        rsync \
        subversion \
        tcl-dev \
        tk-dev \
        x11proto-core-dev \
        xauth \
        xfonts-base \
        xvfb \
        libcairo2-dev \
        libgit2-dev \
        libmysqlclient-dev \
        libpq-dev \
        libsasl2-dev \
        libsqlite3-dev \
        libssh2-1-dev \
        unixodbc-dev \
        fonts-roboto \
        ghostscript \
        hugo \
        less \
        libglpk-dev \
        libgmp3-dev \
        libfribidi-dev \
        libharfbuzz-dev \
        libhunspell-dev \
        libicu-dev \
        liblzma-dev \
        libmagick++-dev \
        libopenmpi-dev \
        libpcre2-dev \
        libssl-dev \
        libv8-dev \
        libxml2-dev \
        libxslt1-dev \
        libzmq3-dev \
        libhdf5-dev \
        qpdf \
        texinfo \
        vim  \
        libcurl4-openssl-dev  \
	libnlopt-dev 



# Install R and pandoc
# Add apt source per the instructions in 
# https://cran.r-project.org/bin/linux/ubuntu/fullREADME.html
RUN  echo "deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/" >> /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9 && \
    apt-get update && \
    apt-get -y install \
        texlive \
        texlive-latex-extra \
        r-base \
        r-base-dev \
        pandoc \
        pandoc-citeproc 

# There is a bug? or a feature, that by default the
# display uses X. We don't have X (currently) asthis
# is a headless application (including rstudio, which
# uses the web not X). There is a way to set the default
# output type to avoid X problems and use cairo:
# https://discourse.osc.edu/t/graphics-display-issues-with-r-built-from-source-for-rstudio-server/1123/5
# options(bitmapType='cairo') to /{RInstallDir}/lib64/R/etc/Rprofile.site.
# You can also add --with-x to the configure.
RUN mkdir -p /usr/local/lib/R/etc && \
    chmod 755 /usr/local/lib/R/etc && \
    echo "options(bitmapType='cairo')" > /usr/local/lib/R/etc/Rprofile.site && \
    chmod 644 /usr/local/lib/R/etc/Rprofile.site

ARG R_HOME=/usr/local/lib/R
ENV CRAN=https://cloud.r-project.org
ENV LC_ALL=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV TZ=America/New_York

ENTRYPOINT ["R"]
