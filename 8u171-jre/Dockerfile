FROM alpine:3.8
MAINTAINER Richard <nibocn@gmail.com>

ENV LANG=en_US.UTF-8

ARG JAVA_VERSION_MAJOR=8
ARG JAVA_VERSION_MINOR=171
ARG JAVA_PACKAGE=jre
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
    curl -o ${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz -L -O -H "Cookie: oraclelicense=accept-securebackup-cookie" -k "http://ftp.wsisiz.edu.pl/pub/pc/pozyteczne%20oprogramowanie/java/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz" && \
    tar xf ${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz -C /opt/java && \
    ln -s /opt/java/jre* /opt/java/jre && \
    ln -s /opt/java/jre /opt/java/jvm && \
    ln -s /opt/java/jre/bin/java /usr/local/bin && \
    apk del glibc-i18n curl ca-certificates && \
    rm -rf /var/cache/apk/* \
    /tmp/* \
    /opt/java/jre/plugin \
    /opt/java/jre/bin/javaws \
    /opt/java/jre/bin/jjs \
    /opt/java/jre/bin/orbd \
    /opt/java/jre/bin/pack200 \
    /opt/java/jre/bin/policytool \
    /opt/java/jre/bin/rmid \
    /opt/java/jre/bin/rmiregistry \
    /opt/java/jre/bin/servertool \
    /opt/java/jre/bin/tnameserv \
    /opt/java/jre/bin/unpack200 \
    /opt/java/jre/lib/javaws.jar \
    /opt/java/jre/lib/deploy* \
    /opt/java/jre/lib/*jfx* \
    /opt/java/jre/lib/amd64/libdecora_sse.so \
    /opt/java/jre/lib/amd64/libprism_*.so \
    /opt/java/jre/lib/amd64/libfxplugins.so \
    /opt/java/jre/lib/amd64/libglass.so \
    /opt/java/jre/lib/amd64/libgstreamer-lite.so \
    /opt/java/jre/lib/amd64/libjavafx*.so \
    /opt/java/jre/lib/amd64/libjfx*.so \
    /opt/java/jre/lib/ext/jfxrt.jar \
    /opt/java/jre/lib/ext/nashorn.jar \
    /opt/java/jre/lib/oblique-fonts \
    /opt/java/jre/lib/plugin.jar

ENV JAVA_HOME=/opt/java/jre
ENV PATH=${PATH}:${JAVA_HOME}/bin
