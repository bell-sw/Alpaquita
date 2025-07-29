# syntax=docker/dockerfile:1

# Image for Go

ARG BASE_IMAGE="bellsoft/alpaquita-linux-base:stream-musl"
FROM "$BASE_IMAGE"

# Whether to remove APK tools from the image
ARG REMOVE_APK_TOOLS="no"

ARG MAINTAINER=""
ARG DESCRIPTION=""

LABEL maintainer="$MAINTAINER"
LABEL org.opencontainers.image.authors="$MAINTAINER"
LABEL org.opencontainers.image.description="$DESCRIPTION"

RUN \
    set -e; command set -o pipefail; \
    case "$REMOVE_APK_TOOLS" in \
        yes|no) ;; \
        *) \
            echo "Invalid REMOVE_APK_TOOLS: '${REMOVE_APK_TOOLS}'. "; \
            echo "Only 'yes' and 'no' are supported."; \
            exit 1; \
            ;; \
    esac; \
    apk add --no-cache \
        bash \
        binutils \
        coreutils \
        findutils \
        g++ \
        gcc \
        go \
        go-doc \
        libc-dev \
        make \
        openssh-client; \
    if [ "$REMOVE_APK_TOOLS" = "yes" ]; then \
        apk del --no-cache apk-tools; \
    fi

# See https://tip.golang.org/doc/go1.20#minor_library_changes
ENV GODEBUG="tarinsecurepath=0,zipinsecurepath=0"
