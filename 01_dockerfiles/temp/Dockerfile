FROM ruby

RUN apt-get update && \
    apt-get upgrade -y && \
    apt install nodejs -y && \
    apt install yarn -y && \
    apt install sqlite3 -y && \
    apt install sqlite3 -y

ONBUILD ADD app /opt/app

WORKDIR /opt/app/
