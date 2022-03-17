FROM openjdk:11-jdk-slim

RUN apt update\
    && apt -y install unzip\
    && apt -y install curl

ENV GHIDRA_URL=https://api.github.com/repos/NationalSecurityAgency/ghidra/releases/latest

RUN curl -L $(curl ${GHIDRA_URL} | grep "browser_download_url" | sed -E 's/.*"([^"]+)".*/\1/')\
    --output /tmp/ghidra.zip

RUN unzip /tmp/ghidra.zip -d /opt/ \
    && mv /opt/ghidra* /opt/ghidra\
    && rm /tmp/ghidra.zip

WORKDIR /opt/ghidra/server

ARG P1
ARG P2
ARG P3

RUN sed -ie "s/wrapper.app.parameter.2=.*/${P1}\n${P2}\n${P3}\n/g" server.conf 

CMD ["./ghidraSvr", "console"]