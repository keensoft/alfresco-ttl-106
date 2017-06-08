Alfresco Content Services - Docker compose
==========================================

This **docker** composition has been created for [Alfresco Tech Talk Live #106](https://www.alfresco.com/events/webinars/tech-talk-live-106-intro-alfresco-content-search-services)

Getting started
---------------

Download [Docker](https://www.docker.com/products/overview). If you are on Mac or Windows, [Docker Compose](https://docs.docker.com/compose) will be automatically installed. On Linux, make sure you have the latest version of [Compose](https://docs.docker.com/compose/install/).

Run in this directory:
```
$ docker-compose up
```

Alfresco Content service will be running at:

* Repository [http://localhost:8080](http://localhost:8080)
* FTP [ftp://localhost:2121](ftp://localhost:2121)
* CIFS [smb://localhost:1445/alfresco](smb://localhost:1445/alfresco)
* IMAP (port 1143)
* SMTP (port 2525)

Architecture
------------

![Architecture diagram](architecture.png)

* `alfresco` service
  - Including a Tomcat app server listening at port 8080
* `db` service
  - Including a PostgreSQL server listening at port 5432
* `solr6` service
  - Including a jetty app server listenting at port 8983
* `libreoffice` service
  - Including a headless server listening at port 8997

*Alfresco Search Services* can be disabled for testing purposes

```
$ docker-compose stop solr6
```

Also *Alfresco Transformation Services* can be disabled

```
$ docker-compose stop libreoffice
```
