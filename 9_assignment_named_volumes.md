### Assginment
* Database upgrade with containers
* Create a `postgres` container with named volume psql-data using `15.1`
* Use Dokcer Hub to learn `VOLUME` path and versions needed to run it
* Check logs, stop container
* Create a new `postgres` container with same named volume using `15.2`
* Check logs to validate

### Answer
```bash
$ docker volume create psql

$ docker run -d --name psql1 -e POSTGRES_PASSWORD=mypassword -v psql:/var/lib/postgresql/data postgres:15.1

$ docker logs psql1

$ docker stop psql1

$ docker run -d --name psql2 -e POSTGRES_PASSWORD=mypassword -v psql:/var/lib/postgresql/data postgres:15.2

$ docker logs psql2

$ docker stop psql2

```