### Assignment

* docs.docer.com and `--help` are your friend
* Run a `nginx`, a `mysql`, and a `httpd`(apache) server
* Run all of them `--detach` (or `-d`), name them with `--name`
* nginx should listen on `80:80`, httpd on `8080:80`, mysql on `3306:3306`
* When running `mysql`, use the `--env` option (or `-e`) to pass in `MYSQL_RANDOM_PORT_PASSWORD=yes`
* Use `docker container log` on mysql to find the random password it created on startup
* Clean it all up with `docker container stop` and `docker container rm` (both can accept multiple names or ID's)
* Use `docker container ls` to ensure everthing is correct before and after cleanup

### Answer

> docker container run -d -p 3306:3306 --name db -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
> docker container logs db

找到 `2024-08-28 17:46:58+00:00 [Note] [Entrypoint]: GENERATED ROOT PASSWORD: gUuJ75TOKqlwgGupSkNNRj+YB7eifste`

> docker container run -d --name webserver -p 8080:80 httpd
> docker container run -d --name proxy -p 80:80 nginx
> docker container stop e0d00560347a 4978a0842f62 07529065b2fe
> docker container rm e0d00560347a 4978a0842f62 07529065b2fe
