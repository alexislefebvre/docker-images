FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y texlive-xetex texlive-lang-french && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/

WORKDIR /data
