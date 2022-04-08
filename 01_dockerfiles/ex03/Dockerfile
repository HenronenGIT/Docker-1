FROM ubuntu

EXPOSE 443 80 22

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y curl && \
    apt-get install -y perl && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends tzdata && \
    apt-get install -y ca-certificates && \
    apt-get install -y sudo && \
    apt-get install -y openssh-server

RUN wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh && \
    chmod 777 script.deb.sh && \
    bash script.deb.sh && \
    apt-get install -y gitlab-ee && \
    mkdir /etc/gitlab/trusted-certs/ && \
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 -subj '/CN=localhost' -keyout /etc/gitlab/trusted-certs/localhost.key -out /etc/gitlab/trusted-certs/localhost.crt && \ 
    echo "external_url \"https://localhost\"" >> /etc/gitlab/gitlab.rb && \
	echo "nginx['ssl_certificate'] = \"/etc/gitlab/trusted-certs/localhost.crt\"" >> /etc/gitlab/gitlab.rb && \
	echo "nginx['ssl_certificate_key'] = \"/etc/gitlab/trusted-certs/localhost.key\"" >> /etc/gitlab/gitlab.rb && \
	echo "gitlab_rails['gitlab_shell_ssh_port'] = 4242" >> /etc/gitlab/gitlab.rb && \
    mkdir -p /var/run/sshd

ENTRYPOINT (/opt/gitlab/embedded/bin/runsvdir-start &) && \
    service ssh restart && \
    gitlab-ctl reconfigure && \
    tail -f /dev/null

# docker build -t ex03 ./
# docker run --name ex03 -d -it --rm -p 80:80 -p 4242:22 -p 443:443 --privileged ex03
# docker logs -f <name of container>
# docker exec -it ex03 sh

# http://localhost:8443/

# git config --global http.sslVerify false

# Fixed ssh service not starting
# mkdir -p /var/run/sshd
