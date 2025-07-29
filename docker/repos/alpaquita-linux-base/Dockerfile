# syntax=docker/dockerfile:1

# Base image

FROM scratch

ARG MINIROOTFS
ARG LIBC

# Space-separated list of APK repos to put into /etc/apk/repositories
ARG APK_REPOS=""
# Space-separated list of locales to install in addition to those
# which come in the minirootfs. For example, "fr_FR.UTF-8 zh_CN.utf8"
ARG LOCALES=""
# Whether to remove APK tools from the image
ARG REMOVE_APK_TOOLS="no"

ARG MAINTAINER=""
ARG DESCRIPTION=""

LABEL maintainer="$MAINTAINER"
LABEL org.opencontainers.image.authors="$MAINTAINER"
LABEL org.opencontainers.image.description="$DESCRIPTION"

ADD "${MINIROOTFS}" /

RUN \
    set -e; command set -o pipefail; \
    rootfs_libc=$(. /etc/os-release; echo $LIBC_TYPE); \
    case "$LIBC" in \
        glibc|musl) \
            if [ "$rootfs_libc" != "$LIBC" ]; then \
                echo "${MINIROOTFS}: got '${rootfs_libc}', expected '${LIBC}'"; \
                exit 1; \
            fi; \
            ;; \
        *) \
            echo -n "Invalid LIBC: '${LIBC}'. "; \
            echo "Only 'glibc' and 'musl' are supported."; \
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
    if [ -n "$APK_REPOS" ]; then \
        printf '%s\n' $APK_REPOS | tee /etc/apk/repositories; \
    fi; \
    if [ "$LIBC" = "musl" ]; then \
        # musl-perf is a musl libc with performance optimizations
        apk add --no-cache musl-perf; \
    fi; \
    if [ "$LIBC" = "glibc" ] && [ -n "$LOCALES" ]; then \
       apk add --no-cache glibc-locales; \
       # This takes less space than the --archive option
       locale-gen --no-archive $LOCALES; \
       apk del --no-cache glibc-locales ; \
       rm -f /etc/locale.gen; \
    fi; \
    if [ "$REMOVE_APK_TOOLS" = "yes" ]; then \
        apk del --no-cache apk-tools; \
    fi

CMD ["/bin/sh"]
