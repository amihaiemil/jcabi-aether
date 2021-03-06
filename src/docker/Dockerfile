# Copyright (c) 2012-2015, jcabi.com
# All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met: 1) Redistributions of source code must retain the above
# copyright notice, this list of conditions and the following
# disclaimer. 2) Redistributions in binary form must reproduce the above
# copyright notice, this list of conditions and the following
# disclaimer in the documentation and/or other materials provided
# with the distribution. 3) Neither the name of the rultor.com nor
# the names of its contributors may be used to endorse or promote
# products derived from this software without specific prior written
# permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
# "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT
# NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND
# FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL
# THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT,
# INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
# (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
# SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
# HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT,
# STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
# ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED
# OF THE POSSIBILITY OF SUCH DAMAGE.

FROM ubuntu:14.04
MAINTAINER Yegor Bugayenko <yegor@teamed.io>
LABEL Description="This is the image for aether.jcabi.com" Vendor="jcabi.com" Version="1.0"
WORKDIR /tmp

ENV DEBIAN_FRONTEND=noninteractive

# UTF-8 locale
RUN locale-gen en_US en_US.UTF-8
RUN dpkg-reconfigure locales
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

# Basic Linux tools
RUN apt-get update && apt-get install -y \
    wget bcrypt curl \
    unzip zip \
    gnupg gnupg2 \
    jq \
    bsdmainutils \
    libxml2-utils \
    build-essential \
    automake autoconf

# Git 2.0
RUN apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository ppa:git-core/ppa
RUN apt-get update && apt-get install -y git git-core

# SSH Daemon
RUN apt-get install -y ssh && \
  mkdir /var/run/sshd && \
  chmod 0755 /var/run/sshd

# Ruby
RUN apt-get install -y libmagic-dev zlib1g-dev
RUN apt-add-repository ppa:brightbox/ruby-ng
RUN apt-get update
RUN apt-get install -y ruby2.2 ruby2.2-dev
RUN gem update
RUN gem install nokogiri
RUN gem install bundler

# Java
RUN apt-get install -y default-jdk
RUN apt-get install -y gdebi && \
  wget --quiet http://ppa.launchpad.net/natecarlson/maven3/ubuntu/pool/main/m/maven3/maven3_3.2.1-0~ppa1_all.deb && \
  gdebi --non-interactive maven3_3.2.1-0~ppa1_all.deb && \
  ln -s /usr/share/maven3/bin/mvn /usr/bin/mvn && \
  rm -rf maven3_3.2.1-0~ppa1_all.deb

# PhantomJS
RUN apt-get install -y phantomjs

# S3cmd for AWS S3 integration
RUN apt-get install -y s3cmd

# NodeJS
RUN apt-get install -y nodejs npm
RUN sudo npm install -g npm
RUN ln -s /usr/bin/nodejs /usr/bin/node

# Clean up
RUN rm -rf /tmp/*
RUN rm -rf /root/.ssh
