FROM mono

#
# Inspired by https://github.com/nickdelgrosso/DockerizeMaxQuant
#
COPY ${APP_IMAGE_DIR}/MaxQuant_1.6.2.10.zip /tmp/ 
RUN apt update && apt install unzip
RUN unzip /tmp/MaxQuant_1.6.2.10.zip -d /tmp \
   && rm /tmp/MaxQuant_1.6.2.10.zip \
   && mkdir -p /opt \
   && mv /tmp/MaxQuant /opt/MaxQuant_1.6.2.10  \
   && ln -s /opt/MaxQuant_1.6.2.10 /opt/MaxQuant

ENTRYPOINT ["mono", "/opt/MaxQuant/bin/MaxQuantCmd.exe"]
CMD ["--help"]
