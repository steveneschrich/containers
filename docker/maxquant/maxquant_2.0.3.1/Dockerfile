FROM mono

#
# Inspired by https://github.com/nickdelgrosso/DockerizeMaxQuant
#
COPY ${APP_IMAGE_DIR}/MaxQuant_2.0.3.1.zip /tmp/ 
RUN apt update && apt install unzip
RUN unzip /tmp/MaxQuant_2.0.3.1.zip -d /tmp \
   && rm /tmp/MaxQuant_2.0.3.1.zip \
   && mkdir -p /opt \
   && mv /tmp/MaxQuant_2.0.3.1 /opt \
   && ln -s /opt/MaxQuant_2.0.3.1 /opt/MaxQuant

ENTRYPOINT ["mono", "/opt/MaxQuant/bin/MaxQuantCmd.exe"]
CMD ["--help"]
