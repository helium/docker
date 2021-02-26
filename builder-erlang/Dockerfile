FROM erlang:23.2.5-alpine as builder

RUN apk add --no-cache --update \
    git tar build-base linux-headers autoconf automake libtool pkgconfig \
    dbus-dev bzip2 bison flex gmp-dev cmake lz4 libsodium-dev openssl-dev \
    sed wget
