# Graylog

Graylog is a leading centralized log management solution for capturing, storing, and enabling real-time analysis of terabytes of machine data.

## Requirements

You will need a fairly recent version of [Docker](https://docs.docker.com/installation/).

We will use the following Docker images in this chapter:

* Graylog: [graylog/graylog](https://hub.docker.com/r/graylog/graylog/)
* MongoDB: [mongo](https://hub.docker.com/_/mongo/)
* Elasticsearch: [docker.elastic.co/elasticsearch/elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/5.5/docker.html)

##  Configurations

Copy `.env.example` file to `.env`.

Graylog comes with a default configuration that works out of the box but you have to set a password for the admin user and the web interface needs to know how to connect from your browser to the Graylog REST API.

In this case you can login to Graylog with the username and password `admin`, use the default `.env` settings.

Generate your own admin password with the following command and put the SHA-256 hash into the `GRAYLOG_ROOT_PASSWORD_SHA2` `.env` variable:

```
echo -n "Enter Password: " && head -1 </dev/stdin | tr -d '\n' | sha256sum | cut -d" " -f1
```

## Setup

Starting Graylog related containers:

```
docker-compose up -d --build graylog
```

After starting Graylog containers by running ``docker-compose up -d --build graylog``, 
you can open the URL `http://127.0.0.1:9000` in a web browser and log in with username `admin` and password `admin` 
(make sure to change the password later). 

Change `GRAYLOG_HTTP_EXTERNAL_URI=` in `.env` file, to your server IP if you run Docker remotely.

Exposed ports:

GRAYLOG_HTTP_PORT       - 9000
GRAYLOG_SYS_TCP_PORT    - 1514
GRAYLOG_SYS_UDP_PORT    - 1514
GRAYLOG_GELF_TCP_PORT   - 12201
GRAYLOG_GELF_UDP_PORT   - 12201

## Links

* https://docs.docker.com/installation/
* https://hub.docker.com/r/graylog/graylog/
* https://hub.docker.com/_/mongo/
* https://www.elastic.co/guide/en/elasticsearch/reference/5.5/docker.html  
* https://docs.graylog.org/en/4.0/pages/installation/docker.html
