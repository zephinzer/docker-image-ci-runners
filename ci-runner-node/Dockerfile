ARG CODENAME="carbon"
FROM zephinzer/alpine-node:latest-${CODENAME}
ENV APK_DEPENDENCIES "bash curl git jq openssh"
RUN apk add --update --upgrade --no-cache ${APK_DEPENDENCIES} 
ADD ./version-info /usr/bin/
WORKDIR ["/"]
ENTRYPOINT ["version-info"]