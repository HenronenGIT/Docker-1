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
ONBUILD RUN rake db:migrate

# docker build -t rails ./
# docker run --name rails -d --rm -it rails
# docker exec -it rails sh