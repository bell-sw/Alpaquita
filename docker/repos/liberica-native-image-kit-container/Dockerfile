# syntax=docker/dockerfile:1

# NIK image

ARG BASE_IMAGE="bellsoft/alpaquita-linux-base:stream-musl"
FROM "$BASE_IMAGE"

# Only 22 is supported
ARG NIK_RELEASE="22"
# 11, 17 are supported
ARG JAVA_RELEASE="17"

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
        22) ;; \
        *) \
            echo -n "Invalid NIK_RELEASE: '${NIK_RELEASE}'. "; \
            echo "Only '22' is supported'."; \
            exit 1; \
            ;; \
    esac; \
    case "$JAVA_RELEASE" in \
        11|17) ;; \
        *) \
            echo -n "Invalid JAVA_RELEASE: '${JAVA_RELEASE}'. "; \
            echo "Only '11' and '17' are supported."; \
            exit 1; \
            ;; \
    esac; \
    apk add --no-cache "liberica-nik-${NIK_RELEASE}-${JAVA_RELEASE}"
