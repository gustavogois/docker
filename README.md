# docker

# spring-boot-mongodb
Project related

## See the logs and running the app

The Mongo's container is running in the background. To see the logs of this container:

```
docker logs -f <container_id>
```

Run the application:

```mvn spring-boot:run```

### Notes

- We're no overriding any properties at all (application.property is empty). We're purely using the spring boot defaults. 
- We're not using the embedded MongoDB.

## Images X Container

- In an analogy, docker images are like java's class, while the container represents the instances of the images.
- An Image defines a Docker container.
- Images are immutable. Once built, the files making up an image do not change.
- Images are built in layers. Each layer is an immutable file (but is a collection of files and directories)
- Layers receive an ID. Thus, if the layer contents change, the ID changes too.

### Notes

- Command to see the mongo's image:

```
docker image inspect mongo
```

- Command to see complet hash ID

```
docker images -q --no-trunc
```

## Persistent

If we stop the container, all registered data are lost. So, what we need is tell it to map to 
a specific directory on the host machine. So, when it starts back up, it will bring the 
database up, just like how it's running on localhost.

1. Create the directory dockerdata/mongo/

2. Remember the command to run mongo image:

```
docker run -p 27017:27017 -d mongo
```

Now, execute this command:

```
docker run -p 27017:27017 -v /Users/gustavogois/projetos/spring-boot-mongodb/dockerdata/mongo:/data/db -d mongo
```

All these information you can find on docker hub mongo's page.

## Rabbit MQ

- ```docker run -d --hostname my-rabbit --name some-rabbit -p 8080:15672 rabbitmq:3-management```

## MYSQL

```
docker run --name gois-mysql2 -v /Users/gustavogois/projetos/spring-boot-mongodb/dockerdata/mysql:/var/lib/mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -p 3306:3306 -d mysql
```

## Notes

- "With a lot of Docker containers, you're going to be setting environment variables, mapping ports, and mapping storage."

### House Keeping

See DockerHouseKeeping.pdf

https://springframework.guru/docker-cheat-sheet-for-spring-devlopers/ 

## Other useful commands

- ```docker kill 749d087e19d9```
- ```docker logs -f 2d829b113cbd```
- ```docker logs 91094e7def43```

- ```lsof -nP -i4TCP:8080 | grep LISTEN```
- ```sudo lsof -iTCP -sTCP:LISTEN -n -P```

- ```kill -9 <<pid>>```

- ```history | grep mongo```
- ```!577```

- ```ls -tlr```

