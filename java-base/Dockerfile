FROM alpine:3.8 

ENV LANG=C.UTF-8

RUN set -eux && \
	apk update && apk upgrade && \
	wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub &&\
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.30-r0/glibc-2.30-r0.apk &&\
    apk --no-cache add unzip vim curl git bash ca-certificates glibc-2.30-r0.apk file && \
	rm -rf /var/lib/apk/* &&\
    mkdir -p /usr/skywalking/agent/

# A streamlined jre
ADD jdk1.8.0_221/ /usr/java/jdk1.8.0_221/

# set env
ENV JAVA_HOME /usr/java/jdk1.8.0_221
ENV PATH ${PATH}:${JAVA_HOME}/bin

# run container with base path:/
WORKDIR /

CMD bash