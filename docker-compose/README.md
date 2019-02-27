# What is docker-compose.yaml file?

A docker-compose.yaml file, is a file in YAML format where you define the different
services involved in your application such as web, database, messaging orchestration
etc..

Once the file is defined, it is easy to bring up the entire stack by running the docker
compose up command.

It has a list of services defined in a key and value format. The key is the name of the
service (This could be anything you want to name your service).

The value of each service must be a dictionary with a minimum specification of an image.
The image could be an image previously built or available on docker hub.


To run the docker compose file type:

```
$ docker-compose up
$ docker-compose stop
```

Run `docker-compose down`  to remove the containers entirely.
