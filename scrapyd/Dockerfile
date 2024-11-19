#
# Dockerfile for scrapyd
#

FROM debian:bookworm
LABEL org.opencontainers.image.authors="Oleg Suvorinov <suvorinovoleg.yandex.ru>"
LABEL org.opencontainers.image.description="Cервис для развертывания и запуска scrapy spider"
LABEL org.opencontainers.image.created="02-10-2024 13:11:08"

ARG TIME_ZONE="Europe/Moscow"
ENV TIME_ZONE=${TIME_ZONE}

SHELL ["/bin/bash", "-c"]

RUN set -xe \
    && apt-get update \
    && apt-get install -y autoconf \
                          build-essential \
                          curl \
                          libffi-dev \
                          libssl-dev \
                          libtool \
                          libxml2 \
                          libxml2-dev \
                          libxslt1.1 \
                          libxslt1-dev \
                          python3 \
                          python3-cryptography \
                          python3-dev \
                          python3-distutils \
                          python3-pil \
                          python3-pip \
                          tini \
                          vim-tiny \
    && rm -f /usr/lib/python3.11/EXTERNALLY-MANAGED \
    && pip install --no-cache-dir dateparser scrapy scrapyd scrapy-poet scrapy-playwright \
    && playwright install firefox \
    && playwright install-deps firefox \
    && mkdir -p /etc/bash_completion.d \
    && curl -sSL https://github.com/scrapy/scrapy/raw/master/extras/scrapy_bash_completion -o /etc/bash_completion.d/scrapy_bash_completion \
    && echo 'source /etc/bash_completion.d/scrapy_bash_completion' >> /root/.bashrc \
    && apt-get purge -y --auto-remove autoconf \
                                      build-essential \
                                      curl \
                                      libffi-dev \
                                      libssl-dev \
                                      libtool \
                                      libxml2-dev \
                                      libxslt1-dev \
                                      python3-dev \
    && apt-get autoclean -y \
    && apt-get clean -y \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/* \
    && cp /usr/share/zoneinfo/$TIME_ZONE /etc/localtime && echo $TIME_ZONE > /etc/timezone

COPY ./scrapyd.conf /etc/scrapyd/
VOLUME /etc/scrapyd/ /var/lib/scrapyd/
EXPOSE 6800

ENTRYPOINT ["tini", "--"]
CMD ["scrapyd", "--pidfile="]