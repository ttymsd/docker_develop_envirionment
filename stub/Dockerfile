FROM ubuntu

MAINTAINER Tetsuya Masuda <ttymsd@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV NODE_ENV development
ENV PORT 8100

EXPOSE 8100

VOLUME ["/documents/api_mock"]
WORKDIR /documents/api_mock

# Install dependencies
RUN apt-get update && \
  apt-get install -yq curl nodejs npm unzip --no-install-recommends && \
  npm cache clean && \
  npm install -g n && \
  npm install -g node-dev && \
  n stable && \
  apt-get purge -yq nodejs npm && \
  apt-get clean

ENTRYPOINT bash
