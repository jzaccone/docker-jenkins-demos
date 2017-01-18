FROM jenkins:1.651.3
 
USER root

RUN apt-get update \
      && apt-get install -y sudo apt-transport-https ca-certificates gnupg2 maven openjdk-8-jdk

RUN echo "deb https://apt.dockerproject.org/repo debian-jessie main" > /etc/apt/sources.list.d/docker.list
RUN apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D


RUN apt-get update \
      && apt-get install -y docker-engine \ 
      && rm -rf /var/lib/apt/lists/*

RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
 
RUN /usr/local/bin/install-plugins.sh docker-workflow workflow-aggregator git
