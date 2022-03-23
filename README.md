Docker-1 - Now, you’re thinking with containers...

12. Launch a phpmyadmin container as a background task. It should be named roach-warden,
its 80 port should be bound to the 8081 port of the virtual machine and it should
be able to explore the database stored in the spawning-pool container.d

docker run --name myadmin -d --link mysql_db_server:db -p 8080:80 phpmyadmin

https://hub.docker.com/r/phpmyadmin/phpmyadmin/
