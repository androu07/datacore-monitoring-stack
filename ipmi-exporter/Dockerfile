FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y ipmitool freeipmi-tools wget tar && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /config
COPY ipmi.yml /config/ipmi.yml

ENV IPMI_VERSION=1.10.1
RUN wget https://github.com/prometheus-community/ipmi_exporter/releases/download/v${IPMI_VERSION}/ipmi_exporter-${IPMI_VERSION}.linux-amd64.tar.gz && \
    tar xvf ipmi_exporter-${IPMI_VERSION}.linux-amd64.tar.gz && \
    mv ipmi_exporter-${IPMI_VERSION}.linux-amd64/ipmi_exporter /usr/local/bin/ && \
    rm -rf ipmi_exporter*

EXPOSE 9290
CMD ["ipmi_exporter", "--config.file=/config/ipmi.yml"]

