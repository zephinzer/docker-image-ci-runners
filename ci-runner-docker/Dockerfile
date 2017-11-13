FROM alpine:3.6
LABEL maintainer="dev@joeir.net" \
      description="Container with Docker capabilities for use in CI pipelines"
ENV APK_DEPENDENCIES="bash curl git jq openssh python py-pip make docker" \
    PIP_DEPENDENCIES="docker-compose"
RUN apk add --update --upgrade --no-cache ${APK_DEPENDENCIES} \
    && pip --no-cache-dir install ${PIP_DEPENDENCIES} \
    && alias md5='md5sum' \
    && rm -rf \
      /var/cache/apk/* \
      /usr/share/man/* \
      ~/.cache/pip/* \
      /var/cache/misc/*
COPY ./version-info /usr/bin/
WORKDIR ["/"]
ENTRYPOINT ["version-info"]