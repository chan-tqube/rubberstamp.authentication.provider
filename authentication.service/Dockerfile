# Authentication Serivce

FROM centos:7

MAINTAINER "Chandresh Rajkumar Manonmani" <chan@tqube.com>

ENV container docker

RUN yum update -y


LABEL organization="Tesark Technologies"

ENV SHELL /bin/bash
RUN timedatectl set-timezone Asia/Kolkata

RUN yum install git -y
RUN yum install -y git-core zlib zlib-devel gcc-c++ patch readline readline-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison curl sqlite-devel

RUN git clone git://github.com/sstephenson/rbenv.git .rbenv
RUN echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
RUN echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
RUN git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
RUN echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bash_profile
RUN source ~/.bash_profile

RUN rbenv install -v 2.2.3
RUN rbenv rehash
RUN rbenv global 2.2.3

RUN gem install bundler

RUN sudo yum install nodejs -y