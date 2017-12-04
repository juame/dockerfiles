FROM jenkinsci/jenkins:2.60.3
LABEL maintainer "Julian Meier <julianmeier@mailtower.ch>"

USER root

# group staff is needed for Mac OS

RUN apt-get update && apt-get install -y apt-utils vim \
	&& curl -sSL https://get.docker.com/ | sh \
	&& usermod -aG docker,staff jenkins \
	&& rm -rf /var/lib/apt/lists/*

USER jenkins
