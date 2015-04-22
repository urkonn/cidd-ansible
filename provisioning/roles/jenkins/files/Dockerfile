FROM jenkins:latest

USER root
RUN groupadd -g 111 docker && usermod -a -G docker jenkins
USER jenkins