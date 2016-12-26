FROM frolvlad/alpine-glibc

MAINTAINER tonywell "tongwei1985@gmail.com"

ARG JAVA_DISTRIBUTION=jdk
ARG JAVA_MAJOR_VERSION=7
ARG JAVA_UPDATE_VERSION=80
ARG JAVA_BUILD_NUMBER=15

ENV JAVA_VERSION=1.${JAVA_MAJOR_VERSION}.0_${JAVA_UPDATE_VERSION}
ENV JAVA_HOME=/opt/java/${JAVA_DISTRIBUTION}${JAVA_VERSION}
ENV PATH=$PATH:$JAVA_HOME/bin

RUN echo "http://mirrors.aliyun.com/alpine/v3.4/main" > /etc/apk/repositories \
    && echo "http://mirrors.aliyun.com/alpine/v3.4/community" >> /etc/apk/repositories \
    && apk add --no-cache --virtual=build-dependencies wget ca-certificates bash tzdata curl && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone && \
	export TINI_VERSION=0.9.0 && \
    export TINI_SHA=fa23d1e20732501c3bb8eeeca423c89ac80ed452 && \
    curl ftp://temp:temp@192.168.50.104/centos7/jenkins/tini-static -o /bin/tini && \
    echo 'Calculated checksum: '$(sha1sum /bin/tini) && \
    chmod +x /bin/tini && echo "$TINI_SHA  /bin/tini" | sha1sum -c - && \
    mkdir -p /opt/java && \
    cd /tmp && \
    wget --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
     http://download.oracle.com/otn-pub/java/jdk/${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-b${JAVA_BUILD_NUMBER}/jdk-${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-linux-x64.tar.gz && \
    tar -xzf jdk-${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-linux-x64.tar.gz -C /opt/java &&\
    ln -s ${JAVA_HOME}/bin/java /usr/bin/java && \ 
    rm -rf ${JAVA_HOME}/*src.zip \
           ${JAVA_HOME}/lib/missioncontrol \
           ${JAVA_HOME}/lib/visualvm \
           ${JAVA_HOME}/lib/*javafx* \
           ${JAVA_HOME}/jre/lib/plugin.jar \
           ${JAVA_HOME}/jre/lib/ext/jfxrt.jar \
           ${JAVA_HOME}/jre/bin/javaws \
           ${JAVA_HOME}/jre/lib/javaws.jar \
           ${JAVA_HOME}/jre/lib/desktop \
           ${JAVA_HOME}/jre/plugin \
           ${JAVA_HOME}/jre/lib/deploy* \
           ${JAVA_HOME}/jre/lib/*javafx* \
           ${JAVA_HOME}/jre/lib/*jfx* \
           ${JAVA_HOME}/jre/lib/amd64/libdecora_sse.so \
           ${JAVA_HOME}/jre/lib/amd64/libprism_*.so \
           ${JAVA_HOME}/jre/lib/amd64/libfxplugins.so \
           ${JAVA_HOME}/jre/lib/amd64/libglass.so \
           ${JAVA_HOME}/jre/lib/amd64/libgstreamer-lite.so \
           ${JAVA_HOME}/jre/lib/amd64/libjavafx*.so \
           ${JAVA_HOME}/jre/lib/amd64/libjfx*.so \
           ${JAVA_HOME}/jre/bin/jjs \
           ${JAVA_HOME}/jre/bin/keytool \
           ${JAVA_HOME}/jre/bin/orbd \
           ${JAVA_HOME}/jre/bin/pack200 \
           ${JAVA_HOME}/jre/bin/policytool \
           ${JAVA_HOME}/jre/bin/rmid \
           ${JAVA_HOME}/jre/bin/rmiregistry \
           ${JAVA_HOME}/jre/bin/servertool \
           ${JAVA_HOME}/jre/bin/tnameserv \
           ${JAVA_HOME}/jre/bin/unpack200 \
           ${JAVA_HOME}/jre/lib/ext/nashorn.jar \
           ${JAVA_HOME}/jre/lib/jfr.jar \
           ${JAVA_HOME}/jre/lib/jfr \
           ${JAVA_HOME}/jre/lib/oblique-fonts \
    apk del build-dependencies && \ 
    rm -rf /tmp/* && \ 
    echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf


