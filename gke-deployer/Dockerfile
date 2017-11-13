# **IMPORTANT**
# The following environmen
FROM iron/base:3.4
LABEL maintainer="dev@joeir.net" \
      description="Google Container Engine deployer container for use in CI pipelines"
ARG GCLOUD_SDK_VERSION="177.0.0"
ARG GCLOUD_SDK_URL="https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${GCLOUD_SDK_VERSION}-linux-x86_64.tar.gz"
ENV APK_DEPENDENCIES="bash curl git jq python py-pip make docker" \
    PIP_DEPENDENCIES="docker-compose" \
    DIR_INSTALL=/tmp
ENV DIR_GCLOUD_SDK=${DIR_INSTALL}/google-cloud-sdk
ENV PATH=${DIR_GCLOUD_SDK}/bin:$PATH
ENV PATHS_TO_REMOVE="\
  /usr/include/* \
  /usr/share/man/* \
  /var/cache/apk/* \
  ~/.cache/pip/*"
RUN apk add --update --upgrade --no-cache ${APK_DEPENDENCIES} \
    && pip --no-cache-dir install ${PIP_DEPENDENCIES} \
    && mkdir -p ${DIR_INSTALL} \
    && curl -o ${DIR_INSTALL}/install.sh https://sdk.cloud.google.com \
    && chmod 550 ${DIR_INSTALL}/install.sh \
    && ${DIR_INSTALL}/install.sh --disable-prompts --install-dir=${DIR_INSTALL} \
    && source ${DIR_GCLOUD_SDK}/path.bash.inc \
    && gcloud config set disable_usage_reporting true \
    && gcloud components install alpha beta container-builder-local docker-credential-gcr kubectl -q \
    && rm -rf ${PATHS_TO_REMOVE}}
ADD ./version-info /usr/bin/
WORKDIR ["/"]
ENTRYPOINT ["version-info"]