
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

* Logs

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

## Configuration
(COPY From bitnami/moodle: [Link](https://github.com/bitnami/containers/tree/main/bitnami/moodle))

### Environment variables

If you want to add a new environment variable:

For docker-compose add the variable name and value under the application section in the docker-compose.yml file present in this repository:

```
moodle:
  ...
  environment:
    - MOODLE_PASSWORD=my_password
  ...
```

Available environment variables:

#### User and Site configuration

`MOODLE_USERNAME:` Moodle application username. Default: user
`MOODLE_PASSWORD:` Moodle application password. Default: bitnami
`MOODLE_EMAIL:` Moodle application email. Default: user@example.com
`MOODLE_SITE_NAME:` Moodle site name. Default: New Site
`MOODLE_SKIP_BOOTSTRAP:` Do not initialize the Moodle database for a new deployment. This is necessary in case you use a database that already has Moodle data. Default: no
`MOODLE_HOST:` Allows you to configure Moodle's wwwroot feature. Ex: example.com. By default it is a PHP superglobal variable. Default: $_SERVER['HTTP_HOST']
`MOODLE_REVERSEPROXY:` Allows you to activate the reverseproxy feature of Moodle. Default: no
`MOODLE_SSLPROXY:` Allows you to activate the sslproxy feature of Moodle. Default: no
`MOODLE_LANG:` Allows you to set the default site language. Default: en

#### Use an existing database

`MOODLE_DATABASE_TYPE:` Database type. Valid values: mariadb, mysqli, pgsql, auroramysql. Default: mariadb
`MOODLE_DATABASE_HOST:` Hostname for database server. Default: mariadb
`MOODLE_DATABASE_PORT_NUMBER:` Port used by database server. Default: 3306
`MOODLE_DATABASE_NAME:` Database name that Moodle will use to connect with the database. Default: bitnami_moodle
`MOODLE_DATABASE_USER:` Database user that Moodle will use to connect with the database. Default: bn_moodle
`MOODLE_DATABASE_PASSWORD:` Database password that Moodle will use to connect with the database. No defaults.
`ALLOW_EMPTY_PASSWORD:` It can be used to allow blank passwords. Default: no


#### Create a database for Moodle using mysql-client


`MYSQL_CLIENT_FLAVOR:` SQL database flavor. Valid values: mariadb or mysql. Default: mariadb.
`MYSQL_CLIENT_DATABASE_HOST:` Hostname for MariaDB server. Default: mariadb
`MYSQL_CLIENT_DATABASE_PORT_NUMBER:` Port used by MariaDB server. Default: 3306
`MYSQL_CLIENT_DATABASE_ROOT_USER:` Database admin user. Default: root
`MYSQL_CLIENT_DATABASE_ROOT_PASSWORD:` Database password for the database admin user. No defaults.
`MYSQL_CLIENT_CREATE_DATABASE_NAME:` New database to be created by the mysql client module. No defaults.
`MYSQL_CLIENT_CREATE_DATABASE_USER:` New database user to be created by the mysql client module. No defaults.
`MYSQL_CLIENT_CREATE_DATABASE_PASSWORD:` Database password for the MYSQL_CLIENT_CREATE_DATABASE_USER user. No defaults.
`MYSQL_CLIENT_CREATE_DATABASE_CHARACTER_SET:` Character set to use for the new database. No defaults.
`MYSQL_CLIENT_CREATE_DATABASE_COLLATE:` Database collation to use for the new database. No defaults.
`MYSQL_CLIENT_CREATE_DATABASE_PRIVILEGES:` Database privileges to grant for the user specified in MYSQL_CLIENT_CREATE_DATABASE_USER to the database specified in MYSQL_CLIENT_CREATE_DATABASE_NAME. No defaults.
`MYSQL_CLIENT_ENABLE_SSL_WRAPPER:` Whether to force SSL connections to the database via the mysql CLI tool. Useful for applications that rely on the CLI instead of APIs. Default: no
`MYSQL_CLIENT_ENABLE_SSL:` Whether to force SSL connections for the database. Default: no
`MYSQL_CLIENT_SSL_CA_FILE:` Path to the SSL CA file for the new database. No defaults
`MYSQL_CLIENT_SSL_CERT_FILE:` Path to the SSL CA file for the new database. No defaults
`MYSQL_CLIENT_SSL_KEY_FILE:` Path to the SSL CA file for the new database. No defaults
`ALLOW_EMPTY_PASSWORD:` It can be used to allow blank passwords. Default: no

#### Create a database for Moodle using postgresql-client

`POSTGRESQL_CLIENT_DATABASE_HOST:` Hostname for the PostgreSQL server. Default: postgresql
`POSTGRESQL_CLIENT_DATABASE_PORT_NUMBER:` Port used by the PostgreSQL server. Default: 5432
`POSTGRESQL_CLIENT_POSTGRES_USER:` Database admin user. Default: root
`POSTGRESQL_CLIENT_POSTGRES_PASSWORD:` Database password for the database admin user. No defaults.
`POSTGRESQL_CLIENT_CREATE_DATABASE_NAMES:` List of new databases to be created by the postgresql-client module. No defaults.
`POSTGRESQL_CLIENT_CREATE_DATABASE_USER:` New database user to be created by the postgresql-client module. No defaults.
`POSTGRESQL_CLIENT_CREATE_DATABASE_PASSWORD:` Database password for the POSTGRESQL_CLIENT_CREATE_DATABASE_USER user. No defaults.
`POSTGRESQL_CLIENT_CREATE_DATABASE_EXTENSIONS:` PostgreSQL extensions to enable in the specified database during the first initialization. No defaults.
`POSTGRESQL_CLIENT_EXECUTE_SQL:` SQL code to execute in the PostgreSQL server. No defaults.
`ALLOW_EMPTY_PASSWORD:` It can be used to allow blank passwords. Default: no


#### SMTP Configuration


To configure Moodle™ to send email using SMTP you can set the following environment variables:

`MOODLE_SMTP_HOST:` SMTP host.
`MOODLE_SMTP_PORT:` SMTP port.
`MOODLE_SMTP_USER:` SMTP account user.
`MOODLE_SMTP_PASSWORD:` SMTP account password.
`MOODLE_SMTP_PROTOCOL:` SMTP protocol.


#### PHP configuration


`PHP_ENABLE_OPCACHE:` Enable OPcache for PHP scripts. No default.
`PHP_EXPOSE_PHP:` Enables HTTP header with PHP version. No default.
`PHP_MAX_EXECUTION_TIME:` Maximum execution time for PHP scripts. No default.
`PHP_MAX_INPUT_TIME:` Maximum input time for PHP scripts. No default.
`PHP_MAX_INPUT_VARS:` Maximum amount of input variables for PHP scripts. No default.
`PHP_MEMORY_LIMIT:` Memory limit for PHP scripts. Default: 256M
`PHP_POST_MAX_SIZE:` Maximum size for PHP POST requests. No default.
`PHP_UPLOAD_MAX_FILESIZE:` Maximum file size for PHP uploads. No default.



## Maintenance

### Backing up your container

To backup your data, configuration and logs, follow these simple steps:

#### Step 1: Stop the currently running container

```
docker compose stop moodle
```

#### Step 2: Run the backup command

We need to mount two volumes in a container we will use to create the backup: a directory on your host to store the backup in, and the volumes from the container we just stopped so we can access the data.

```
docker run --rm -v /path/to/moodle-backups:/backups --volumes-from moodle busybox \
  cp -a /bitnami/moodle /backups/latest
```

### Restoring a backup

Restoring a backup is as simple as mounting the backup as volumes in the containers.

For the MariaDB database container:

```
 $ docker run -d --name mariadb \
   ...
-  --volume /path/to/mariadb-persistence:/bitnami/mariadb \
+  --volume /path/to/mariadb-backups/latest:/bitnami/mariadb \
   bitnami/mariadb:latest
```

For the Moodle™ container:

```
 $ docker run -d --name moodle \
   ...
-  --volume /path/to/moodle-persistence:/bitnami/moodle \
+  --volume /path/to/moodle-backups/latest:/bitnami/moodle \
   bitnami/moodle:latest
```


