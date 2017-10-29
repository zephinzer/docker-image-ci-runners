FROM zephinzer/alpine-node:latest-carbon
ENV APK_DEPENDENCIES "bash curl git jq make openssh python py-pip docker"
ENV PIP_DEPENDENCIES "docker-compose"
RUN apk add --update --upgrade --no-cache ${APK_DEPENDENCIES} 
RUN pip install ${PIP_DEPENDENCIES}