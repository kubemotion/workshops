FROM jenkins/jenkins:2.89.3-alpine

# Jenkins plugins installation
RUN /usr/local/bin/install-plugins.sh ssh-slaves \
 && /usr/local/bin/install-plugins.sh kubernetes
