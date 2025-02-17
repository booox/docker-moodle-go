# docker-compose-moodle
Deploy Moodle with Docker compose


## Quick Start

```
# Clone
$ git clone https://github.com/booox/docker-moodle-go.git
$ cd docker-compose-moodle

# Change USER & PASSWORD
$ vi .composeenv


# Run Docker Compose
$ docker compose up -d
```

## Set Folder

```
sudo chown -R 1001:1001 ./backupData/mariadb/
sudo chmod -R 750 ./backupData/mariadb/
```

If not working, down the docker compose and remove containers.

```
docker compose down -v
```

Then up again.

```
docker compose up -d
```

Wait a few minutes, and Access the home page.

Access your application at [http://your-ip:8080](http://your-ip:8080)
