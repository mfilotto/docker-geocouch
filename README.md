# Dockerized GeoCouch

## Work in Progress


To be used like:

```
git clone https://github.com/14mmm/docker-geocouch.git
cd docker-geocouch
docker build -t 14mmm/geocouch(:<version>) .
docker run -d -p 5984:5984 14mmm/geocouch
```

To attach an 'inspection container' to the VOLUME paths from the Dockerfile do:

```
docker ps # to look up the actual container's name
docker run -i --volumes-from="<container name>" -t ubuntu /bin/bash
```

Use `docker logs <container name>` to get look at Stdout from the container.

## Not yet investigated

* https://github.com/jhs/build-couchdb
* http://rcouch.org/

---

### Comments welcome.

---

Original README.md below

---

YADC
===

Yet Another Dockerized CouchDB.
Put the couch in a docker container and ship it anywhere.

If you're looking for a CouchDB with SSL support you can check out [klaemo/couchdb-ssl](https://index.docker.io/u/klaemo/couchdb-ssl/)

Version: `CouchDB 1.6.0`

## Run

Available in the docker index as [klaemo/couchdb](https://index.docker.io/u/klaemo/couchdb/)

```bash
[sudo] docker pull klaemo/couchdb

# expose it to the world on port 5984
[sudo] docker run -d -p 5984:5984 -name couchdb klaemo/couchdb

curl http://localhost:5984
```

## Features

* exposes couchdb on port `5984` of the container
* runs everything as user `couchdb` (security ftw!)
* keeps couchdb running with `mon` (reliability ftw!)

## Build your own

You can use `klaemo/couchdb` as the base image for your own couchdb instance.
You might want to provide your own version of the following files:

* `local.ini` for CouchDB

Example Dockerfile:
```
FROM klaemo/couchdb

ADD local.ini /usr/local/etc/couchdb/
```

and then build and run

```
[sudo] docker build -rm -t you/awesome-couchdb .
[sudo] docker run -d -p 5984:5984 -v ~/couchdb:/usr/local/var/lib/couchdb you/awesome-couchdb
```
