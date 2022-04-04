FROM ruby

RUN apt-get update && \
    apt-get upgrade -y && \
    apt install nodejs -y && \
    apt install yarn -y && \
    apt install rails -y && \
    apt install sqlite3 -y

ONBUILD ADD app /opt/app
ONBUILD WORKDIR /opt/app

ONBUILD EXPOSE 3000
ONBUILD RUN bundle install
ONBUILD RUN rake db:migrate

# docker build -t rails:on-build ./
# docker run --name rails -p 3000:3000 -d --rm -it rails:on-build
# docker exec -it rails sh
