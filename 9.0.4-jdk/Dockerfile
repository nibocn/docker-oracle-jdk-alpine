FROM alpine:3.8
MAINTAINER Richard <nibocn@gmail.com>

ENV LANG=C.UTF-8

ARG JAVA_VERSION=9.0.4
ARG JAVA_PACKAGE=jdk
ARG GLIBC_PKG_VERSION=2.28-r0

RUN cd /tmp && \
    apk add --no-cache --update-cache curl ca-certificates bash && \
    curl -Lo /etc/apk/keys/sgerrand.rsa.pub "https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub" && \
    curl -Lo glibc-${GLIBC_PKG_VERSION}.apk "https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_PKG_VERSION}/glibc-${GLIBC_PKG_VERSION}.apk" && \
    curl -Lo glibc-bin-${GLIBC_PKG_VERSION}.apk "https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_PKG_VERSION}/glibc-bin-${GLIBC_PKG_VERSION}.apk" && \
    curl -Lo glibc-i18n-${GLIBC_PKG_VERSION}.apk "https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_PKG_VERSION}/glibc-i18n-${GLIBC_PKG_VERSION}.apk" && \
    apk add glibc-${GLIBC_PKG_VERSION}.apk glibc-bin-${GLIBC_PKG_VERSION}.apk glibc-i18n-${GLIBC_PKG_VERSION}.apk && \
    /usr/glibc-compat/bin/localedef --force --inputfile POSIX --charmap UTF-8 "$LANG" || true && \
    echo "export LANG=$LANG" > /etc/profile.d/locale.sh && \
    mkdir -p /opt/java && \
    curl -o ${JAVA_PACKAGE}-${JAVA_VERSION}_linux-x64_bin.tar.gz -L -O -H "Cookie: oraclelicense=accept-securebackup-cookie" -k "http://ftp.wsisiz.edu.pl/pub/pc/pozyteczne%20oprogramowanie/java/${JAVA_VERSION}/${JAVA_PACKAGE}-${JAVA_VERSION}_linux-x64_bin.tar.gz" && \
    tar xf ${JAVA_PACKAGE}-${JAVA_VERSION}_linux-x64_bin.tar.gz -C /opt/java && \
    ln -s /opt/java/jdk* /opt/java/jdk && \
    ln -s /opt/java/jdk /opt/java/jvm && \
    ln -s /opt/java/jdk/bin/java /usr/local/bin && \
    ln -s /opt/java/jdk/bin/javac /usr/local/bin && \
    apk del glibc-i18n curl ca-certificates && \
    rm -rf /var/cache/apk/* \
    /tmp/* \
    /opt/java/jdk/*src.zip \
    /opt/java/jdk/lib/missioncontrol \
    /opt/java/jdk/lib/visualvm \
    /opt/java/jdk/lib/*javafx* \
    /opt/java/jdk/jre/plugin \
    /opt/java/jdk/jre/bin/javaws \
    /opt/java/jdk/jre/bin/jjs \
    /opt/java/jdk/jre/bin/orbd \
    /opt/java/jdk/jre/bin/pack200 \
    /opt/java/jdk/jre/bin/policytool \
    /opt/java/jdk/jre/bin/rmid \
    /opt/java/jdk/jre/bin/rmiregistry \
    /opt/java/jdk/jre/bin/servertool \
    /opt/java/jdk/jre/bin/tnameserv \
    /opt/java/jdk/jre/bin/unpack200 \
    /opt/java/jdk/jre/lib/javaws.jar \
    /opt/java/jdk/jre/lib/deploy* \
    /opt/java/jdk/jre/lib/desktop \
    /opt/java/jdk/jre/lib/*javafx* \
    /opt/java/jdk/jre/lib/*jfx* \
    /opt/java/jdk/jre/lib/amd64/libdecora_sse.so \
    /opt/java/jdk/jre/lib/amd64/libprism_*.so \
    /opt/java/jdk/jre/lib/amd64/libfxplugins.so \
    /opt/java/jdk/jre/lib/amd64/libglass.so \
    /opt/java/jdk/jre/lib/amd64/libgstreamer-lite.so \
    /opt/java/jdk/jre/lib/amd64/libjavafx*.so \
    /opt/java/jdk/jre/lib/amd64/libjfx*.so \
    /opt/java/jdk/jre/lib/ext/jfxrt.jar \
    /opt/java/jdk/jre/lib/ext/nashorn.jar \
    /opt/java/jdk/jre/lib/oblique-fonts \
    /opt/java/jdk/jre/lib/plugin.jar

ENV JAVA_HOME=/opt/java/jdk
ENV PATH=${PATH}:${JAVA_HOME}/bin
