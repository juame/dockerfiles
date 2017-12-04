FROM centos:6
LABEL maintainer "Julian Meier <julianmeier@mailtower.ch>"

RUN groupadd -g 1000 jenkins \
	&& useradd -d "/home/jenkins" -u 1000 -g 1000 -m -s /bin/bash jenkins

RUN yum groupinstall -y "Development Tools" --exclude=git \
  && yum install -y \
    epel-release \
    yum-utils \
    rpmdevtools \
    rpmlint \
    yum-utils \
    rpmdevtools \
    rpmlint \
    wget \
    rsync \
    which \
    tree \
    libevent-devel \
    zlib-devel \
    perl-ExtUtils-MakeMaker \
    asciidoc \
    xmlto \
    openssl-devel \
    curl-devel \
    expat-devel \
    gettext-devel \
  && yum clean all

RUN curl -sSL -o /tmp/git.tar.gz https://github.com/git/git/archive/v2.15.1.tar.gz \
  && mkdir -p /usr/src/git \
  && tar -xzf /tmp/git.tar.gz -C /usr/src/git --strip-components 1 \
  && rm -f /tmp/git.tar.gz \
  && ( \
    cd /usr/src/git \
    && make configure \
    && ./configure --prefix=/usr/local \
    && make all doc \
    && make install install-doc install-html \
  ) \
  && rm -rf /usr/src/git

RUN curl --silent --location https://rpm.nodesource.com/setup_6.x | bash - \
	&& yum -y install nodejs \
	&& yum clean all

RUN wget https://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm \
  && yum localinstall -y erlang-solutions-1.0-1.noarch.rpm \
  && rm -f erlang-solutions-1.0-1.noarch.rpm \
  && yum install -y esl-erlang-20.1-1 \
  && yum clean all

RUN curl -sSL -o /tmp/rebar3.tar.gz https://github.com/erlang/rebar3/archive/3.4.7.tar.gz \
  && mkdir -p /usr/src/rebar3 \
  && tar -xzf /tmp/rebar3.tar.gz -C /usr/src/rebar3 --strip-components 1 \
  && rm -f /tmp/rebar3.tar.gz \
  && ( \
    cd /usr/src/rebar3 \
    && ./bootstrap \
    && mv rebar3 /usr/local/bin \
  ) \
  && rm -rf /usr/src/rebar3

USER jenkins
