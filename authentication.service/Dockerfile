# Authentication Serivce (authentication.service)

FROM centos:7

MAINTAINER "Chandresh Rajkumar Manonmani" <chan@tqube.com>

ENV container docker
ENV APP_NAME authentication.service
ENV APP_USER $APP_NAME
ENV APP_GROUP $APP_NAME
ENV APP_PATH /${APP_NAME}

LABEL organization="Tesark Technologies"

RUN yum update -y

RUN yum install git -y
RUN yum install -y git-core zlib zlib-devel gcc-c++ patch readline readline-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison curl sqlite-devel
RUN yum clean all 

RUN groupadd $APP_GROUP; useradd -g $APP_GROUP --home-dir $APP_PATH $APP_USER
USER $APP_USER
ENV HOME $APP_PATH

ENV RBENV_ROOT ${HOME}/.rbenv
ENV PATH ${RBENV_ROOT}/bin:${RBENV_ROOT}/shims:$PATH

RUN git clone git://github.com/sstephenson/rbenv.git ${RBENV_ROOT}
RUN git clone git://github.com/sstephenson/ruby-build.git ${RBENV_ROOT}/plugins/ruby-build
RUN echo 'eval "$(rbenv init -)"' >> ~/.bash_profile

ONBUILD USER $APP_USER

ONBUILD COPY .ruby-version ${APP_PATH}/
ONBUILD WORKDIR $APP_PATH
ONBUILD ENV CONFIGURE_OPTS --disable-install-doc
ONBUILD RUN rbenv install -v 2.2.3
ONBUILD RUN rbenv rehash
ONBUILD RUN rbenv global 2.2.3

ONBUILD RUN mkdir $( dirname $(ruby -e 'print Gem::ConfigFile::SYSTEM_WIDE_CONFIG_FILE') )
ONBUILD RUN echo 'gem: --no-document' >> $(ruby -e 'print Gem::ConfigFile::SYSTEM_WIDE_CONFIG_FILE')

ONBUILD RUN gem install bundler
ONBUILD RUN rbenv rehash

ONBUILD RUN sudo yum install nodejs -y

ONBUILD USER root

ONBUILD ENV PORT 8080

ONBUILD COPY . $APP_PATH
ONBUILD RUN chown $APP_USER -R $APP_PATH

ONBUILD USER $APP_USER
ONBUILD WORKDIR $APP_PATH

ONBUILD RUN bundle install

ONBUILD EXPOSE $PORT
ONBUILD CMD bundle exec rails s -p $PORT
