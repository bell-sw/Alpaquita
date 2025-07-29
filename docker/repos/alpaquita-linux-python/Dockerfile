# syntax=docker/dockerfile:1

# Python 3 image

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
    apk add --no-cache python3 py3-pip py3-wheel py3-setuptools; \
    if [ "$REMOVE_APK_TOOLS" = "yes" ]; then \
        apk del --no-cache apk-tools; \
    fi
