FROM rocker/r-base:4.1.2

###########################################################################
# Add Moffitt's Certs
###########################################################################

RUN wget -c http://plsa0001/download/moffitt_certs/moffitt-ca.cer -O /usr/local/share/ca-certificates/moffitt-ca.crt --no-check-certificate && wget -c http://plsa0001/download/moffitt_certs/moffitt-ca-int.cer -O /usr/local/share/ca-certificates/moffitt-ca-int.crt --no-check-certificate && update-ca-certificates


###########################################################################
# Set Timezone
###########################################################################

ARG TZ=America/New_York
ENV TZ ${TZ}

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
