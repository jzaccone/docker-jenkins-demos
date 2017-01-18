FROM jenkins:1.651.3
 
USER root

RUN apt-get update \
      && apt-get install -y openjdk-8-jdk \
      && rm -rf /var/lib/apt/lists/*

RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
 
RUN /usr/local/bin/install-plugins.sh docker-plugin jclouds-jenkins token-macro durable-task

# Copy in the Docker certs, we'll use /usr/local/etc for them
#COPY certs/ca-key.pem /usr/local/etc/jenkins/certs/ca-key.pem
COPY certs/ca.pem /usr/local/etc/jenkins/certs/ca.pem
COPY certs/cert.pem /usr/local/etc/jenkins/certs/cert.pem
COPY certs/key.pem /usr/local/etc/jenkins/certs/key.pem
COPY certs/key.pem /usr/local/etc/jenkins/certs/server-key.pem
COPY certs/key.pem /usr/local/etc/jenkins/certs/server.pem


# Make sure cert permissions are set correctly
RUN chmod +r /usr/local/etc/jenkins/certs/ca.pem
RUN chmod +r /usr/local/etc/jenkins/certs/cert.pem
RUN chmod +r /usr/local/etc/jenkins/certs/key.pem
RUN chmod +r /usr/local/etc/jenkins/certs/server-key.pem
RUN chmod +r /usr/local/etc/jenkins/certs/server.pem
RUN chown -R jenkins:jenkins /usr/local/etc/jenkins

USER jenkins
