# syntax=docker/dockerfile:1

# Image with GDB

ARG BASE_IMAGE="bellsoft/alpaquita-linux-base:stream-musl"
FROM "$BASE_IMAGE"

# Space-separated list of packages
ARG PKGS="\
    gdb\
"

ARG MAINTAINER=""
ARG DESCRIPTION=""

LABEL maintainer="$MAINTAINER"
LABEL org.opencontainers.image.authors="$MAINTAINER"
LABEL org.opencontainers.image.description="$DESCRIPTION"

RUN \
    set -e; command set -o pipefail; \
    apk add --no-cache $PKGS
