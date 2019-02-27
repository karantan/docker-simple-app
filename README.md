# Docker basic commands

```
$ docker ps
$ docker ps -a
$ docker run ubuntu
$ docker stop <container>
$ docker rm [containers ...]
$ docker images
$ docker rmi [images ...]
```

Run in background - deteched
```
$ docker run -d myweb-app
```

Map the port from the container to the docker host
```
$ docker run -p 80:5000 myweb-app
```

Run the command inside the container

```
$ docker exec -it <container> bash
```

Volume mapping

```
$ docker run -v /opt/datadir:/var/lib/mysql mysql
```

Here we create /opt/datadir on the docker host and map it to /var/lib/mysql folder inside
the container.


See details of a container (e.g. internal IP)

```
$ docker inspect <container>
```

# Build the image

```
$ docker build . -t karantan/simple-web-app
$ docker images
$ docker push karantan/simple-web-app
```

Before you push the image you might need to do `docker login`.


# Run the container

```
$ docker run -it -p 6543:6543 karantan/simple-web-app
```


# Run vs Command vs Entrypoint

In a nutshell

- `RUN` executes command(s) in a new layer and creates a new image.
  E.g., it is often used for installing software packages.
- `CMD` sets default command and/or parameters, which can be overwritten from command
  line when docker container runs.
- `ENTRYPOINT` configures a container that will run as an executable.

Example:

```
FROM ubuntu

ENTRYPOINT ["sleep"]

CMD ["5"]
```

If you run `docker run ubuntu-sleep` (assuming `ubuntu-sleep` is the image name) then
this container will sleep for 5 seconds. But you can also run it like this:
`docker run ubuntu-sleep 10`. The `10` will overwrite the CMD and the container will
sleep for 10 seconds.

# ENV Variable in Docker

Add `-e` option when you run the container:

```
$ docker run -e APP_COLOR=blue karantan/simple-web-app
```


# Docker networks

1. Bridge
2. None
3. Host


## Bridge

The Bridge network is a private internal network created by Docker on the host. All the
containers attached to this network by default and they get an internal IP address
usually in the range 172.17 series. The containers can access each other using this
internal IP if required. To access any of these containers from the outside world,
you must map ports of these containers to the docker host (e.g. `-p 6543:6543`).


## Host
Another way to access the containers externally is to associate the containers
to the host network.

This takes out any network isolation between the docker host and the docker container.
Meaning if you were to run a web server on port 5000 in a web-app container, it is
automatically accessible on the same port externally without requiring any port mapping
as the web container uses the host network.

This would also mean that unlike before, you will now not be able to run multiple web
containers on the same host on the same port as the ports are now common to all
containers in the host network.

## None

With the none network, containers are not a task to any network and doesn't have any
access to the external network or other containers.


## User defined networks

You can also define your own networks:

```
$ docker network create --driver bridge --subnet 182.18.0.0/16 custom-isolated-network
$ docker network ls
```
