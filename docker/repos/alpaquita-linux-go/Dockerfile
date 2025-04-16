# syntax=docker/dockerfile:1

# Image for Go

ARG BASE_IMAGE="bellsoft/alpaquita-linux-base:stream-musl"
FROM "$BASE_IMAGE"

ARG MAINTAINER=""
ARG DESCRIPTION=""

LABEL maintainer="$MAINTAINER"
LABEL org.opencontainers.image.authors="$MAINTAINER"
LABEL org.opencontainers.image.description="$DESCRIPTION"

RUN \
    set -e; command set -o pipefail; \
    apk add --no-cache \
        bash \
        binutils \
        coreutils \
        findutils \
        g++ \
        gcc \
        git \
        go \
        go-doc \
        libc-dev \
        make \
        openssh-client

# See https://tip.golang.org/doc/go1.20#minor_library_changes
ENV GODEBUG="tarinsecurepath=0,zipinsecurepath=0"
