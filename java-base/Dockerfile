FROM alpine:3.10 as base

ENV LANG=en_US.UTF-8

# Here I install GNU libc (aka glibc) and set en_US.UTF-8 locale and set TZ Asia/Shanghai as default.

RUN ALPINE_GLIBC_PUB_URL="https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub" && \
    ALPINE_GLIBC_BASE_URL="https://github.com/sgerrand/alpine-pkg-glibc/releases/download" && \
    ALPINE_GLIBC_PACKAGE_VERSION="2.30-r0" && \
    ALPINE_GLIBC_BASE_PACKAGE_FILENAME="glibc-$ALPINE_GLIBC_PACKAGE_VERSION.apk" && \
    ALPINE_GLIBC_BIN_PACKAGE_FILENAME="glibc-bin-$ALPINE_GLIBC_PACKAGE_VERSION.apk" && \
    ALPINE_GLIBC_I18N_PACKAGE_FILENAME="glibc-i18n-$ALPINE_GLIBC_PACKAGE_VERSION.apk" && \
    apk add --no-cache --virtual=.build-dependencies wget ca-certificates && \
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub "$ALPINE_GLIBC_PUB_URL" && \
    wget \
        "$ALPINE_GLIBC_BASE_URL/$ALPINE_GLIBC_PACKAGE_VERSION/$ALPINE_GLIBC_BASE_PACKAGE_FILENAME" \
        "$ALPINE_GLIBC_BASE_URL/$ALPINE_GLIBC_PACKAGE_VERSION/$ALPINE_GLIBC_BIN_PACKAGE_FILENAME" \
        "$ALPINE_GLIBC_BASE_URL/$ALPINE_GLIBC_PACKAGE_VERSION/$ALPINE_GLIBC_I18N_PACKAGE_FILENAME" && \
    apk add --no-cache \
        tzdata unzip vim curl git bash \
        "$ALPINE_GLIBC_BASE_PACKAGE_FILENAME" \
        "$ALPINE_GLIBC_BIN_PACKAGE_FILENAME" \
        "$ALPINE_GLIBC_I18N_PACKAGE_FILENAME" && \
    \
    /usr/glibc-compat/bin/localedef -i en_US -f UTF-8 en_US.UTF-8 && \
    rm "/etc/apk/keys/sgerrand.rsa.pub" && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    \
    apk del glibc-i18n && \
    \
    rm "/root/.wget-hsts" && \
    apk del .build-dependencies && \
    rm \
        "$ALPINE_GLIBC_BASE_PACKAGE_FILENAME" \
        "$ALPINE_GLIBC_BIN_PACKAGE_FILENAME" \
        "$ALPINE_GLIBC_I18N_PACKAGE_FILENAME"
		
# Here I download oracle JDK8
FROM base 

# streamlined jre
ADD jdk-8u221-linux-x64.tar.gz /usr/java/

# set env
ENV JAVA_HOME /usr/java/jdk1.8.0_221
ENV PATH ${PATH}:${JAVA_HOME}/bin
#
# run container with base path:/
WORKDIR /