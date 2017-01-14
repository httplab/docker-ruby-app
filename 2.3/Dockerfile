FROM httplab/ruby:2.3-centos7

ENV LOCALE=en_US.utf8
ENV LANGUAGE=$LOCALE
ENV LANG=$LOCALE
ENV LC_ALL=$LOCALE

RUN gem update --system $RUBYGEMS_VERSION
RUN gem install bundler

ENV USER apps
ENV APP app

ENV GEM_HOME /.gem
ENV PATH $GEM_HOME/bin:$PATH
ENV BUNDLE_APP_CONFIG $GEM_HOME

RUN yum -y groupinstall "Development Tools"
RUN yum -y install postgresql-devel sudo vim iputils

ENV HOME /home/$USER
RUN useradd $USER
RUN usermod -aG wheel $USER
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

RUN mkdir -p $GEM_HOME && chown -R $USER $GEM_HOME

RUN mkdir $HOME/$APP
WORKDIR $HOME/$APP

RUN chown $USER:$USER $HOME/$APP

ENV TZ=Europe/Moscow
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
