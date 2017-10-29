FROM zephinzer/alpine-node:latest-boron
ENV APK_DEPENDENCIES "bash curl git jq openssh"
RUN apk add --update --upgrade --no-cache ${APK_DEPENDENCIES} 
ADD ./version-info /usr/bin/
WORKDIR ["/"]
ENTRYPOINT ["version-info"]