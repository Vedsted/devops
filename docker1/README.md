# Docker exercise

If you are unable to do any of the tasks asked of you here, then please provide a description of what you have _tried_ to do, or what you would do _if it worked_.

## The gay border TOIlet

The TOIlet (stands for “The Other Implementation’s letters”) application is a linux CLI that takes the input characters and produces various text-based effects. I want a container that can output me colorful variations of a given text.

See [TOIlet's website](http://caca.zoy.org/wiki/toilet) for more info (but you do not have to).

**Tasks:**

Write a build file that:

* takes an ubuntu 18.04
* instals toilet.
* makes sure that the commands `toilet -F border --gay` always will be run before any user inputted commands to the container.

Submit your build file.

Build your image, calling it `<yourusername>/toilet`.

Push your newly created image up to dockerhub, and provide the link to it.

<br>

### Solution:
Github page: https://github.com/Vedsted/devops/tree/master/docker1/toilet  
Docker image: https://hub.docker.com/r/vedsted/toilet/ 

Dockerfile:
```docker
    FROM    ubuntu:18.04
    RUN     apt-get update -y && apt-get upgrade -y && apt-get install toilet -y
    CMD     toilet -F border --gay

``` 
<br><br>

## Wordpress with proxy

We want to run a wordpress site, that sits behind a proxy server. You do not need any experience with proxies, nor Nginx in particular to solve this assignment.

You need to provide a docker compose file with the following containers in:

* Nginx as a proxy (in the script called loadbalancer-nginx)
* Mysql as a database (in the script called db)
* Wordpress as an application (in the script called wordpress)

**Tasks:**

* Make nginx the only container visible to the outside world, and only on port 80.
* Make the containers start in the following order: mysql,wordpress,nginx
* Make nginx volume in the file `nginx.conf` on the container path /etc/nginx/conf.d/default.conf
* Make wordpress and mysql configured so they do not need to ask for database host, database name, user and password (hint: look at their docker-hub pages)
* Make a network that all containers belong to.

Describe what kind of commands you would use to delete the containers and create new ones.

Describe where you would define what exact version of mysql docker should use?

What commands will give you the ip addresses of the containers in the described network.

<br>

### Solution:

Docker-compose file: [docker-compose.yml](https://github.com/Vedsted/devops/blob/master/docker1/wordpress/docker-compose.yml)

<br>

* *Describe what kind of commands you would use to delete the containers and create new ones.*
    * the command below starts the network with all the associated containers:  
        ```docker-compose up -d```

    * the command below stops the network and the associated containers:  
        ```docker-compose down```

* *Describe where you would define what exact version of mysql docker should use?*
    * the version of mysql is defined together with the image in the docker-compose file.  
        In the example below, the mysql version is set to 5.7:

```yml
# mysql container
  db:
    image: mysql:5.7
    environment:
      - MYSQL_ROOT_PASSWORD=wordpress
    networks:
      - if_wordpress
```


* *What commands will give you the ip addresses of the containers in the described network.*   
    * the command ```docker network inspect <network-name>```, will display the information about the network and the assosiated containers.
