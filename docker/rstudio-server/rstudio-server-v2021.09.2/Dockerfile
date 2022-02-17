FROM dockerhub.moffitt.org/hpc/r:4.1

LABEL maintainer="Steven.Eschrich@moffitt.org"
LABEL version="0.1"
LABEL description="This is a base Ubuntu 20.04 image with basic tools."

# Disable Prompt During Packages Installation
ARG DEBIAN_FRONTEND=noninteractive  

# Update Ubuntu Software repository
RUN apt update && \
   wget --no-check-certificate -O /usr/local/share/ca-certificates/moffitt-ca-int.crt \
      "https://gitlab.moffitt.usf.edu:8000/singularity/mcc-certificates/-/raw/main/certs/moffitt-ca-int.cer" && \

   wget --no-check-certificate -O /usr/local/share/ca-certificates/moffitt-ca.crt \
      "https://gitlab.moffitt.usf.edu:8000/singularity/mcc-certificates/-/raw/main/certs/moffitt-ca.cer"  && \
	wget --no-check-certificate -O /usr/local/share/ca-certificates/moffitt-chain \
      "https://gitlab.moffitt.usf.edu:8000/singularity/mcc-certificates/-/raw/main/certs/moffitt-chain" && \
 

# From https://www.rstudio.com/products/rstudio/download-server/debian-ubuntu/
   apt-get install -y gdebi-core && \
   wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-2021.09.2-382-amd64.deb && \
   gdebi -n rstudio-server-2021.09.2-382-amd64.deb 
   # Disabled due to an error saying the server is running, not sure why.
   #/usr/lib/rstudio-server/bin/rstudio-server verify-installation 


ARG R_HOME=/usr/local/lib/R
ENV CRAN=https://cloud.r-project.org
ENV CRAN_SOURCE=https://cloud.r-project.org
ENV LC_ALL=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV TZ=America/New_York

# This starts the server listening on a random port (see the qsub
# submission script). The port only works on localhost, so that
# ssh tunneling is required.
ENTRYPOINT ["/usr/lib/rstudio-server/bin/rserver"]
CMD ["--www-port", "$RSTUDIO_PORT", "--www-address", "127.0.0.1"]
