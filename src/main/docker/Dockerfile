FROM jenkins/jenkins:2.71-alpine
MAINTAINER youhouhouhou

#https://github.com/jenkinsci/docker/blob/master/README.md



USER root
# see: http://wiki.alpinelinux.org/wiki/Setting_the_timezone
RUN echo "https://mirror.tuna.tsinghua.edu.cn/alpine/v3.4/main" > /etc/apk/repositories && \
    echo "https://mirror.tuna.tsinghua.edu.cn/alpine/v3.4/community" >> /etc/apk/repositories && \
    echo "https://mirror.tuna.tsinghua.edu.cn/alpine/edge/testing/" >> /etc/apk/repositories && \
    apk --update add tzdata && \
    apk add libstdc++ bash aria2 && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone && \
    apk del tzdata && \
    rm -rf /tmp/* /var/cache/apk/* && \
    echo "UTC+8:00" > /etc/TZ
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8


USER ${user}


#ENV JENKINS_UC_DOWNLOAD https://mirrors.tuna.tsinghua.edu.cn/jenkins

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

#COPY https.pem /var/lib/jenkins/cert
#COPY https.key /var/lib/jenkins/pk
#ENV JENKINS_OPTS --httpPort=-1 --httpsPort=8083 --httpsCertificate=/var/lib/jenkins/cert --httpsPrivateKey=/var/lib/jenkins/pk
#EXPOSE 8083

#ENV JENKINS_SLAVE_AGENT_PORT 50001


COPY init/executors.groovy /usr/share/jenkins/ref/init.groovy.d/executors.groovy
#COPY custom.groovy /usr/share/jenkins/ref/init.groovy.d/custom.groovy
