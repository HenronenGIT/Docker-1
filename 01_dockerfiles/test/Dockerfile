FROM ruby:3.1.0

RUN apt update -y &&\
	apt install -y nodejs &&\
	rm -rf /var/lib/apt/lists/*

WORKDIR /opt/app

ONBUILD COPY . /opt/app
ONBUILD RUN gem install bundler
ONBUILD RUN bundle install
ONBUILD RUN rails db:create
ONBUILD RUN rails db:migrate
