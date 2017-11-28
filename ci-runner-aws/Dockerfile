# **IMPORTANT**
# The following environmen
FROM iron/base:3.4
LABEL maintainer="dev@joeir.net" \
      description="Amazon Web Services deployer container for use in CI pipelines"
ENV APK_DEPENDENCIES="bash curl git jq python py-pip make docker" \
    PIP_DEPENDENCIES="awscli"
ENV PATHS_TO_REMOVE="\
  /usr/include/* \
  /usr/share/man/* \
  /var/cache/apk/* \
  ~/.cache/pip/*"
RUN apk update \
    && apk upgrade \
    && apk add --no-cache ${APK_DEPENDENCIES} \
    && pip --no-cache-dir install ${PIP_DEPENDENCIES}
ADD ./version-info /usr/bin/
WORKDIR ["/"]
ENTRYPOINT ["version-info"]