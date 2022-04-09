# Docker-1 - Now, you’re thinking with containers...

> *Virtual machine virtualizes hardware, Docker virtualizes Operating system.*
> 

!! - 

# PDF

[docker-1.en.pdf](Docker-1%20-%2090ab6/docker-1.en.pdf)

[Docker_Eval_Form](Docker-1%20-%2090ab6/Intra_Projects_docker-1_Edit.pdf)

---

## Commands

`docker start` - run already renamed/created container

`docker ps [-a] [-q]`  - view running docker

`docker pull` - pull dockers from dockerhub

`docker exec -it <name of the container> bash` - access the container shell

`docker run -d -t —-name “rename your docker” <name of image>` - run docker image

`docker pull “docker hub link”:version` - pull different version of the docker image

`docker stop <name of the docker>` - stop container

`docker -d` - run container in a background

`docker ps -a` - see traces of all containers

`docker inspect <name_of_volume>` - see location of volume

---

# Exercises

### **For each exercise, we will ask you to give the shell command(s) to:**

- [x]  Get the hello-world container from the Docker Hub, where it’s available.
    
    `docker pull hello-world`
    
- [x]  Launch the hello-world container, and make sure that it prints its welcome mes-
sage, then leaves it.
    
    `docker run hello-world`
    
- [x]  Launch a nginx container, available on Docker Hub, as a background task. It
should be named overlord, be able to restart on its own, and have its 80 port
attached to the 5000 port of your machine. You can check that your container
functions properly by visiting http://localhost:5000 on your web browser.
    
    `docker run --restart=always -d -p 5000:80 --name overlord nginx`
    
    - Test with [http://localhost:5000/](http://localhost:5000/)
- [x]  Get the internal IP address of the overlord container without starting its shell and
in one command.
- [x]  Launch a shell from an alpine container, and make sure that you can interact
directly with the container via your terminal, and that the container deletes itself
once the shell’s execution is done.
- [x]  From the shell of a debian container, install via the container’s package manager
everything you need to compile C source code and push it onto a git repo (of
course, make sure before that the package manager and the packages already in the
container are updated). For this exercise, you should only specify the commands
to be run directly in the container.
- [x]  Create a volume named hatchery.
    - `docker volume ls`
- [x]  List all the Docker volumes created on the machine. Remember. VOLUMES.
- [x]  Launch a mysql container as a background task. It should be able to restart on its
own in case of error, and the root password of the database should be Kerrigan.
You will also make sure that the database is stored in the hatchery volume, that
the container directly creates a database named zerglings, and that the container
itself is named spawning-pool.
    
    `docker exec -it spawning-pool mysql -uroot -p`
    
    In mySQL
    
    `SHOW DATABASES;`
    
    [Start containers automatically](https://docs.docker.com/config/containers/start-containers-automatically/)
    
    [Mysql - Official Image | Docker Hub](https://hub.docker.com/_/mysql/)
    
- [x]  Print the environment variables of the spawning-pool container in one command,
to be sure that you have configured your container properly.
- [x]  Launch a wordpress container as a background task, just for fun. The container
should be named lair, its 80 port should be bound to the 8080 port of the virtual
machine, and it should be able to use the spawning-pool container as a database
service. You can try to access lair on your machine via a web browser, with the
IP address of the virtual machine as a URL. Congratulations, you just deployed a
functional Wordpress website in two commands!
    - Username and password can be adde
    
    ### Hostname
    
    `docker inspect spawning-pool | grep name` 
    
- [x]  12. Launch a phpmyadmin container as a background task. It should be named roach-warden,
its 80 port should be bound to the 8081 port of the virtual machine and it should
be able to explore the database stored in the spawning-pool container.d
    
    `docker run --name myadmin -d --link mysql_db_server:db -p 8080:80 phpmyadmin`
    
    [Docker Hub](https://hub.docker.com/r/phpmyadmin/phpmyadmin/)
    
- [x]  13. Look up the spawning-pool container’s logs in real time without running its shell.
    
    `docker logs —-follow <container ID>`
    
- [x]  14. Display all the currently active containers on your machine
    
    `docker ps`
    
- [x]  15. Relaunch the overlord container.
    
    `docker restart <container name>`
    
- [x]  16. Launch a container name Abathur. It will be a Python container, 2-slim version,
its /root folder will be bound to a HOME folder on your host, and its 3000 port
will be bound to the 3000 port of your virtual machine. You will personalize this
container so that you can use the Flask micro-framework in its latest version. You
will make sure that an html page displaying "Hello World" with tags can be
served by Flask. You will test that your container is properly set up by accessing,
via curl or a web browser, the IP address of your virtual machine on the 3000 port.
You will also list all the necessary commands in your repository.

[](https://flask.palletsprojects.com/en/1.0.x/quickstart/)

[Use bind mounts](https://docs.docker.com/storage/bind-mounts/)

1.  Create a local swarm, your local machine (the school iMac) should be its manager

`docker swarm init --advertise-addr <MANAGERS_IP>`  

[Create a swarm](https://docs.docker.com/engine/swarm/swarm-tutorial/create-swarm/)

1.  Create a virtual machine with virtualbox, just like you did in roger-skyline-1.
Make sure the VM’s networking works both ways with your local machine. Make
sure you install and configure Docker to work on the VM.

[Install Docker Engine on Debian](https://docs.docker.com/engine/install/debian/)

1.   ~~Turn the VM you made into a slave of the local swarm in which your local machine
is the leader (the command to take control of the VM is not requested).~~
    
    `docker swarm init --advertise-addr <MANAGERS_IP>`
    
    ![Untitled](Docker-1%20-%2090ab6/Untitled.png)
    
    `sudo docker swarm join-token worker` - show **worker** join token
    
    `sudo docker swarm join-token manager` - show **manager** join token
    
    `docker node ls` - show node status
    
    `docker swarm join -token <manager or worker>` - show join token
    
2. Create an overlay-type internal network that you will name overmind.
    1. `docker network create -d overlay overmind`
3. Launch a rabbitmq SERVICE that will be named orbital-command. You should
define a specific user and password for the RabbitMQ service, they can be whatever
you want. This service will be on the overmind network.
    
    
4. List all the services of the local swarm.
    1. `docker service ls`
5. ~~Launch a 42school/engineering-bay service in two replicas and make sure that
the service works properly (see the documentation provided at [hub.docker.com](http://hub.docker.com/)).
This service will be named engineering-bay and will be on the overmind network.~~
    1. 

~~24. Get the real-time logs of one the tasks of the engineering-bay service.~~

1.  
1. ..~~. Damn it, a group of zergs is attacking orbital-command, and shutting down
the engineering-bay service won’t help at all... You must send a troup of Marines
to eliminate the intruders. Launch a 42school/marine-squad in two replicas,
and make sure that the service works properly (see the documentation provided
at [hub.docker.com](http://hub.docker.com/)). This service will be named... marines and will be on the
overmind network.~~
    1. 
2. ~~Display all the tasks of the marines service.~~
    1. `docker service ps marines`
3. ~~Increase the number of copies of the marines service up to twenty, because there’s
never enough Marines to eliminate Zergs. (Remember to take a look at the tasks
and logs of the service, you’ll see, it’s fun.)~~
    1. `docker service scale -d marines=20`
    
    [docker service scale](https://docs.docker.com/engine/reference/commandline/service_scale/)
    
4. ~~Force quit and delete all the services on the local swarm, in one command.~~
    1. `docker service rm $(docker service ls -q)`
5. ~~Force quit and delete all the containers (whatever their status), in one command.~~
    1. `docker container rm --force $(docker container ls --all -q)`
6. ~~Delete all the container images stored on your local machine machine, in one command as well.~~
    1. `docker image rm $(docker images --all -q`)

# Dockerfiles

### ex00

- [x]  From an alpine image you’ll add to your container your favorite text editor, vim or
emacs, that will launch along with your container.

```docker
FROM alpine
RUN apk update && apk upgrade && \
    apk add vim

CMD vim

# docker build . -t <name_of_image>
# docker run -it <name_of_image>
```

### ex01

`docker run -it -e TS3SERVER_LICENSE=accept ts3 sh`

`ENTRYPOINT`

- When running/entering container - this is what is going to be executed

[How to Install TeamSpeak on Debian 10](https://linuxhint.com/install-teamspeak-debian-10/)

### ex02

- [x]  You are going to create your first Dockerfile to containerize Rails applications. That’s
a special configuration: this particular Dockerfile will be generic, and called in another
Dockerfile, that will look something like this:

```docker
FROM ft-rails:on-build
EXPOSE 3000
CMD ["rails", "s", "-b", "0.0.0.0", "-p", "3000"]
```

- [ ]  Your generic container should install, via a ruby container, all the necessary dependencies and gems, then copy your rails application in the /opt/app folder of your
container. Docker has to install the approtiate gems when it builds, but also launch
the migrations and the db population for your application. The child Dockerfile should
launch the rails server (see example below). If you don’t know what commands to use,
it’s high time to look at the Ruby on Rails documentation.

### Pushing to Dockerhub

1. Create repository in Dockerhub
2. login to Dockerhub trough terminal with a command `login`
3. Rename Docker image you exactly same as in Dockerhub
4.  `docker push henronen/ft_rails:on-build`

### Verify depencies

`ruby --version`

`yarn --version`

`node --version`

`sqlite3 --version`

`rails --version`

`bundle-install` - Install the dependencies specified in your Gemfile

### 

### ONBUILD <instructions>

> *This is useful if you are building an image which will be used as a base to build other images, for example an application build environment or a daemon which may be customized with user-specific configuration.*
> 

> Once the **dependencies** are installed on our **base image** the remaining instructions on our `Dockerfile` will use the [ONBUILD](https://docs.docker.com/engine/reference/builder/#onbuild)
 directive. All the instructions we add using this directive, will be triggered after, when the **child image** is build. It's as if we were placing this instructions in the downstream image, right after its [FROM](https://docs.docker.com/engine/reference/builder/#from) directive.
> 

[Ruby on Rails Guides: Migrations](https://guides.rubyonrails.org/v3.2/migrations.html)

[Getting Started with Rails - Ruby on Rails Guides](https://guides.rubyonrails.org/getting_started.html)

### ex03

`sudo gitlab-ctl reconfigure` - Reconfigure Gitlab

> Docker can be useful to test an application that’s still being developed without polluting your libraries. You will have to design a Dockerfile that gets the development
version of Gitlab - Community Edition installs it with all the dependencies and the necessary configurations, and launches the application, all as it builds. The container will be
deemed valid if you can access the web client, create users and interact via GIT with this
container (HTTPS and SSH). Obviously, you are not allowed to use the official container
from Gitlab, it would be a shame...
> 

- Because the hostname in our example is `gitlab.example.com`, Omnibus GitLab will look for private key and public certificate files called `/etc/gitlab/ssl/gitlab.example.com.key`
 and `/etc/gitlab/ssl/gitlab.example.com.crt`, respectively.
- **If the `certificate.key` file is password protected**, NGINX will not ask for the password when you reconfigure GitLab. In that case, Omnibus GitLab will fail silently with no error messages.

[SSL Configuration | GitLab](https://docs.gitlab.com/omnibus/settings/ssl.html#lets-encrypt-integration)

### curl vs wget

> *The main difference between them is that curl will show the output in the console. On the other hand, wget will download it into a file.*
> 

[SSL Configuration | GitLab](https://docs.gitlab.com/omnibus/settings/ssl.html)

[Download and install GitLab](https://about.gitlab.com/install/#ubuntu)

---

# Links

[How to Docker · VBrazhnik/docker-1 Wiki](https://github.com/VBrazhnik/docker-1/wiki/How-to-Docker)

### Best practices

[Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

### Docker documentation

[Docker Documentation](https://docs.docker.com/)

### You need to learn Docker right now

[https://youtu.be/eGz9DS-aIeY?t=714](https://youtu.be/eGz9DS-aIeY?t=714)

![Untitled](Docker-1%20-%2090ab6/Untitled%201.png)

# Introduction

- Docker makes it easier to share your - lets say an App you have made
- App splitting to microservices.
