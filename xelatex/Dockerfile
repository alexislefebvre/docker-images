FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update \
    && apt install -qy \
    texlive-xetex \
    texlive-lang-french \
    fontconfig \
    && rm -rf /var/lib/apt/lists/* /var/cache/apt/

COPY $PWD /sources

RUN mkdir -p /usr/local/share/fonts/ms_fonts \
    && cp -n /sources/template-resources/fonts/*.ttf /usr/local/share/fonts/ms_fonts/ \
    && fc-cache

WORKDIR /sources

ENTRYPOINT [ "sh", "-c", "xelatex main && xelatex main" ]
