# syntax=docker/dockerfile:1

# Image for C/C++ development with GCC

ARG BASE_IMAGE="bellsoft/alpaquita-linux-base:stream-musl"
FROM "$BASE_IMAGE"

# Space-separated list of packages
ARG PKGS="\
    autoconf\
    automake\
    bash\
    binutils\
    bzip2\
    bzip2-dev\
    curl\
    curl-dev\
    diffutils\
    file\
    findutils\
    fortify-headers\
    g++\
    gawk\
    gcc\
    gdb\
    git\
    grep\
    hexdump\
    jpeg-dev\
    krb5-dev\
    libc-dev\
    libevent-dev\
    libffi-dev\
    libjpeg-turbo-dev\
    libpng-dev\
    libtool\
    libxml2-dev\
    libxslt-dev\
    make\
    ncurses-dev\
    openssl-dev\
    patch\
    pkgconf\
    readline-dev\
    sed\
    subversion\
    unzip\
    xz\
    xz-dev\
    yaml-dev\
    zlib-dev\
"

ARG MAINTAINER=""
ARG DESCRIPTION=""

LABEL maintainer="$MAINTAINER"
LABEL org.opencontainers.image.authors="$MAINTAINER"
LABEL org.opencontainers.image.description="$DESCRIPTION"

RUN \
    set -e; command set -o pipefail; \
    apk add --no-cache $PKGS
