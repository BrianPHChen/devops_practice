### Health Check

* docker engine will `exec` the command in the container
* it expects exit 0 (OK) or exit 1 (Error)
* three container states: starting, healthy, unhealthy

* Healthcheck status shows up in `docker container ls`
* Docker run does nothing with healthcheck
* Services will replace tasks if they fail healthcheck
* Services updates wait for them before continuing

### Example

> docker container run --name p1 -d postgres

> docker container run --name p2 -d --health-cmd="pg_isready -U postgres || exit 1" postgres

如果用inspect查看 會看到health logs

> docker service create --name p1 postgres

> docker service create --name p2 -d --health-cmd="pg_isready -U postgres || exit 1" postgres