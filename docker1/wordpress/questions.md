# Docker-Compose questions


#### Describe what kind of commands you would use to delete the containers and create new ones.

the command below starts the network with the associated containers:

```docker-compose up -d``` 

the command below stops the network and the associated containers:

```docker-compose down```

#### Describe where you would define what exact version of mysql docker should use?

the version of mysql is defined together with the image in the docker-compose file.

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


#### What commands will give you the ip addresses of the containers in the described network.

the command ```docker network inspect <network-name>``` will display information about the network and the assosiated containers.
