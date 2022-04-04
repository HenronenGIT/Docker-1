FROM ubuntu

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y curl && \
    apt-get install -y perl && \
    apt-get install -y vim && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends tzdata && \
    apt-get install -y ca-certificates && \
    apt-get install -y sudo && \
    apt-get install -y openssh-server
    
RUN echo "postfix postfix/mailname string root@localhost" | debconf-set-selections && \
    echo "postfix postfix/main_mailer_type string 'Internet Site'" | debconf-set-selections && \
    apt install -y postfix

RUN wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh && \
    chmod 777 script.deb.sh && \
    bash script.deb.sh && \
    apt-get install -y gitlab-ee

ENTRYPOINT (/opt/gitlab/embedded/bin/runsvdir-start &) && \
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -subj '/CN=localhost' -keyout /etc/gitlab/trusted-certs/localhost.key -out /etc/gitlab/trusted-certs/localhost.crt && \ 
gitlab-ctl reconfigure && tail -f /dev/null

# docker build -t ex03 ./
# docker run --name ex03 -d -it --rm -p 8080:80 -p 8022:22 -p 8443:443 --privileged -e EXTERNAL_URL="https://localhost" ex03
# docker run --name ex03 -d -it --rm -p 8080:80 -p 8022:22 -p 8443:443 -e EXTERNAL_URL="'https://localhost'" --privileged ex03
# docker logs -f <name of container>
# docker exec -it ex03 sh
# http://localhost:8080/