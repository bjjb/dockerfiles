Wordpress
=========

A starting point for a Wordpress site. Starts MySQL and Apache (with PHP) in
the same container, using Supervisor, on Ubuntu 14.04.

Ideally, MySQL would be in another container, but this is simpler for a start.

Alternatively...
----------------

A better solution is to launch mysql in one container and wordpress in
another. You can do this from the command line as follows:

```
docker pull wordpress:latest
docker pull mysql:latest
docker run --name mysqlwp \
            -e MYSQL_ROOT_PASSWORD=wordpressdocker \
            -e MYSQL_DATABASE=wordpress \
            -e MYSQL_USER=wordpress \
            -e MYSQL_PASSWORD=wordpresspwd \
            -v /home/docker/mysql:/var/lib/mysql \
            -d mysql
docker run --name wordpress --link mysqlwp:mysql -p 80:80 \
            -e WORDPRESS_DB_NAME=wordpress \
            -e WORDPRESS_DB_USER=wordpress \
            -e WORDPRESS_DB_PASSWORD=wordpresspwd \
            -d wordpress
```

Change the environment variables as desired.

Check the [mysql Dockerfile](http://bit.ly/mysql-dockerfile); you'll see that
/var/lib/mysql on the local host is mounted as a volume, and we can mount this
on /home/docker/mysql (or wherever we like), allowing us to (for example)
perform a backup with

```
docker exec mysqlwp mysqldump --all-databases \
                              --password=wordpressdocker > wordpress.backup
```
