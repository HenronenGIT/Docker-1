FROM ruby

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt install nodejs -y && \
    apt install yarn -y && \
    apt install rails -y && \
    apt install sqlite3 -y && \
    apt install npm -y

ONBUILD WORKDIR /opt/app
ONBUILD COPY test_app /opt/app

ONBUILD RUN npm install --global yarn
ONBUILD RUN bundle install --without production
ONBUILD RUN rails db:migrate

ONBUILD EXPOSE 3000

# docker build -t ft_rails:on-build ft_rails
# docker build -t 

# docker run --name rails -p 3000:3000 -d --rm -it ft_rails:on-build
# docker exec -it ft_rails sh

# test app https://github.com/mhartl/sample_app_6th_ed
