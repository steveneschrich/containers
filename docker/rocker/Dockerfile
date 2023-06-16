FROM rocker/rstudio:latest

# Disable Prompt During Packages Installation
ARG DEBIAN_FRONTEND=noninteractive  

# Update Ubuntu Software repository
RUN apt update && \
    apt install -y wget ca-certificates locales &&  \
    wget --no-check-certificate \
                -O /usr/local/share/ca-certificates/moffitt-ca-int.crt \
               "https://gitlab.moffitt.usf.edu:8000/singularity/mcc-certificates/-/raw/main/certs/moffitt-ca-int.cer" && \

    wget --no-check-certificate \
                -O /usr/local/share/ca-certificates/moffitt-ca.crt \
                "https://gitlab.moffitt.usf.edu:8000/singularity/mcc-certificates/-/raw/main/certs/moffitt-ca.cer"  && \
    wget --no-check-certificate \
                -O /usr/local/share/ca-certificates/moffitt-chain \
                "https://gitlab.moffitt.usf.edu:8000/singularity/mcc-certificates/-/raw/main/certs/moffitt-chain" && \
    chmod 644 /usr/local/share/ca-certificates/moffitt* && \
        # Given the new certificates in /usr/share/ca-certificates,
        # dkpg-reconfigure regenerates the /etc/ca-certificates.conf to
        # pick them up. Then, run update-ca-certificates to install in
        # /etc/ssl. This seems a bit round-about.
        #dpkg-reconfigure ca-certificates
    update-ca-certificates --verbose && \
    echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen en_US.utf8 && update-locale LANG=en_US.UTF-8 && \
    sed -i 's/^\[system_default_sect\]/\[system_default_sect\]\nOptions = UnsafeLegacyRenegotiation/' /usr/lib/ssl/openssl.cnf 

RUN apt-get -y install \
	texlive \
	texlive-latex-extra

# Add in dvc (data version control)
# https://github.com/iterative/dvc
RUN wget -q --no-check-certificate \
  	 https://github.com/iterative/dvc/releases/download/2.57.1/dvc_2.57.1_amd64.deb && \
        dpkg -i dvc_2.57.1_amd64.deb

ENV CRAN=https://cloud.r-project.org
ENV LC_ALL=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV TZ=America/New_York

