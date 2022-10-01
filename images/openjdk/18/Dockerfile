FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive
RUN export DEBIAN_FRONTEND

RUN groupadd -g 1000 app \
 && useradd -g 1000 -u 1000 -d /var/www -s /bin/bash app

RUN apt-get update && apt-get install -y \
    curl \
    cron \
    git \
    wget \
    gzip \
    libbz2-dev \
    libfreetype6-dev \
    libicu-dev \
    libmcrypt-dev \
    libpng-dev \
    libssh2-1-dev \
    libxslt1-dev \
    libzip-dev \
    lsof \
    default-mysql-client \
    vim \
    zip

RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y openjdk-17-jdk openjdk-17-jre

RUN apt-get update \
    && wget https://dlcdn.apache.org/maven/maven-3/3.8.6/binaries/apache-maven-3.8.6-bin.tar.gz -P /tmp \
    && tar xf /tmp/apache-maven-*.tar.gz -C /opt && rm /tmp/apache-maven-*.tar.gz \
    && ln -s /opt/apache-maven-* /opt/maven

ENV M2_HOME /opt/maven
ENV MAVEN_HOME /opt/maven

RUN export M2_HOME
RUN export MAVEN_HOME


RUN apt-get update \
    && wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.67/bin/apache-tomcat-9.0.67.tar.gz -P /tmp \
    && mkdir /opt/tomcat && tar xzvf /tmp/apache-tomcat-9*tar.gz -C /opt/tomcat --strip-components=1 && rm /tmp/apache-tomcat-9.0.67.tar.gz

RUN chown -R app:app /opt/tomcat/ \
    && chmod -R u+x /opt/tomcat/bin

ENV PATH ${M2_HOME}/bin:${PATH}

RUN export PATH

RUN mkdir -p /etc/nginx/html /var/www/html /sock \
  && chown -R app:app /etc/nginx /var/www /sock

USER app:app

VOLUME /var/www

WORKDIR /var/www/html
EXPOSE 9001

CMD tail -f /dev/null