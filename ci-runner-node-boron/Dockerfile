FROM zephinzer/alpine-node:latest-boron
LABEL maintainer="dev@joeir.net" \
      description="Node Boron container for use in CI pipelines"
ENV APK_DEPENDENCIES="bash curl git jq openssh python py-pip make docker" \
    PIP_DEPENDENCIES="docker-compose"
RUN apk add --update --upgrade --no-cache ${APK_DEPENDENCIES} \
    && pip --no-cache-dir install ${PIP_DEPENDENCIES}
ADD ./version-info /usr/bin/
WORKDIR ["/"]
ENTRYPOINT ["version-info"]