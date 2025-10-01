# syntax=docker/dockerfile:1

# NIK image

ARG BASE_IMAGE="bellsoft/alpaquita-linux-base:stream-musl"
FROM "$BASE_IMAGE"

# 23, 24, 25 are supported
ARG NIK_RELEASE="25"
# 17, 21, 22, 23, 24, 25 are supported
ARG JAVA_RELEASE="25"
# Debug image includes additional components for debugging
ARG IS_DEBUG_IMAGE="no"
# Whether to remove APK tools from the image
ARG REMOVE_APK_TOOLS="no"

ARG MAINTAINER=""
ARG DESCRIPTION=""

LABEL maintainer="$MAINTAINER"
LABEL org.opencontainers.image.authors="$MAINTAINER"
LABEL org.opencontainers.image.description="$DESCRIPTION"

ENV LANG=en_US.UTF-8 LANGUAGE=en_US:en
ENV JAVA_HOME="/usr/lib/jvm/liberica-nik-${NIK_RELEASE}-${JAVA_RELEASE}"

RUN \
    set -e; command set -o pipefail; \
    case "$NIK_RELEASE" in \
        23|24|25) ;; \
        *) \
            echo -n "No NIK_RELEASE '${NIK_RELEASE}'. "; \
            exit 1; \
            ;; \
    esac; \
    case "${NIK_RELEASE}_${JAVA_RELEASE}" in \
        23_17|23_21|24_22|24_23|24_24|25_25) ;; \
        *) \
            echo -n "No JAVA_RELEASE '${JAVA_RELEASE}' for NIK_RELEASE '${NIK_RELEASE}'. "; \
            exit 1; \
            ;; \
    esac; \
    case "$REMOVE_APK_TOOLS" in \
        yes|no) ;; \
        *) \
            echo "Invalid REMOVE_APK_TOOLS: '${REMOVE_APK_TOOLS}'. "; \
            echo "Only 'yes' and 'no' are supported."; \
            exit 1; \
            ;; \
    esac; \
    apk add --no-cache "liberica-nik-${NIK_RELEASE}-${JAVA_RELEASE}"; \
    if [ "$IS_DEBUG_IMAGE" = "yes" ]; then \
        apk add --no-cache maven gdb; \
    fi; \
    if [ "$REMOVE_APK_TOOLS" = "yes" ]; then \
        apk del --no-cache apk-tools; \
    fi
