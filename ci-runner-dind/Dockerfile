FROM docker:latest
LABEL maintainer="dev@joeir.net" \
      description="Docker-in-Docker container for use in CI pipelines"
ENV APK_DEPENDENCIES="bash curl git jq openssh build-base python-dev python py-pip make" \
    PIP_DEPENDENCIES="docker-compose"
RUN apk add --update --upgrade --no-cache ${APK_DEPENDENCIES}} \
    && pip --no-cache-dir install ${PIP_DEPENDENCIES}} \
    && alias md5='md5sum' \
    && rm -rf \
      /var/cache/apk/* \
      /usr/share/man/* \
      ~/.cache/pip/* \
      /var/cache/misc/*
COPY ./version-info /usr/bin/
WORKDIR ["/"]
ENTRYPOINT ["version-info"]
VOLUME ["/var/run/docker.sock", "/cache"]