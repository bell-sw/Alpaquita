# syntax=docker/dockerfile:1

# Python 3 image

ARG BASE_IMAGE="bellsoft/alpaquita-linux-base:stream-musl"
FROM "$BASE_IMAGE"

ARG MAINTAINER=""
ARG DESCRIPTION=""

LABEL maintainer="$MAINTAINER"
LABEL org.opencontainers.image.authors="$MAINTAINER"
LABEL org.opencontainers.image.description="$DESCRIPTION"

RUN \
    set -e; command set -o pipefail; \
    apk add --no-cache python3 py3-pip py3-wheel py3-setuptools
