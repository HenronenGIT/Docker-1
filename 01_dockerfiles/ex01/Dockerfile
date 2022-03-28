FROM debian

EXPOSE 9987/udp \
    30033/tcp \
    10011/tcp

RUN mkdir teamspeak3

WORKDIR /teamspeak3/

RUN apt-get update && \
    apt-get upgrade -y && \
    apt install wget -y && \
    apt install bzip2 -y && \
    apt install net-tools -y && \
    wget https://files.teamspeak-services.com/releases/server/3.13.3/teamspeak3-server_linux_amd64-3.13.3.tar.bz2


RUN tar -xvf teamspeak3-server_linux_amd64-3.13.3.tar.bz2

WORKDIR /teamspeak3/teamspeak3-server_linux_amd64/

CMD sh ts3server_startscript.sh start

# docker build ./ -t ts3
# We need to add enviroment variable to accept term of services!
# docker run -p 9987:9987/udp -p 10011:10011 -p 30033:30033 -it -e TS3SERVER_LICENSE=accept ts3

NOT STAYING ON!