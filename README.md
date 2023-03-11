
# docker-moodle-go
Deploy Moodle with Docker compose


## Quick Start

```
# Clone
$ git clone https://github.com/booox/docker-moodle-go.git
$ cd docker-moodle-go

# Change USER & PASSWORD
$ vi docker-compose.yml


# Run Docker Compose
$ docker compose up -d
```


Wait a few minutes, and Access the home page.

Change localhost  if necessary.
[http://localhost:8080](http://localhost:8080)



## Commands

* Check Tools

```
$ docker compose ps
$ docker compose logs
$ docker compose logs moodle
$ docker compose --help
```

* Start & Stop

```
$ docker compose up -d
$ docker compose stop
```

