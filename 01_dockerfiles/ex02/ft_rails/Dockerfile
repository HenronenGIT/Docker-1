FROM ruby:2.7

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt install nodejs -y && \
    apt install yarn -y && \
    apt install rails -y && \
    apt install sqlite3 -y && \
    apt install npm -y

ONBUILD ADD test_app /opt/app
ONBUILD WORKDIR /opt/app

ONBUILD RUN npm install --global yarn
ONBUILD RUN bundle install --without production
ONBUILD RUN rails db:migrate
ONBUILD RUN bundle exec rails webpacker:install

ONBUILD EXPOSE 3000

# docker build -t ft-rails:on-build ft_rails
# docker build -t ex02 ./

# docker run --name ex02 -p 3000:3000 -d --rm -it ex02
# docker exec -it ex02 sh

# test app https://github.com/mhartl/sample_app_6th_ed
