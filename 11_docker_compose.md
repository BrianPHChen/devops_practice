### Docker Compose
- YAML-formatted file that describes the solution options for:
  - containers
  - networks
  - volumes
- A CLI tool docker-compose used for local dev/test automation with those YAML files
- Compose YAML has its own version: 1, 2, 2.1, 3.1
- YAML can be used with `docker-compose` command for local docker automation
- With `docker` directly in production with Swarm (as of v1.13)
- docker-compose --help
- `docker-compose.yml` is default filename, but any can be used with `docker-compose -f`

> `docker-compose` now can change to `docker compose`

### Docker Compose CLI
- Two most common commands are
  - `docker compose up` 如果加上 `-d` 在後面就會跑在背景
  - `docker compose down`
- if all your projects had a `Dockerfile` and `docker-compose.yml` then "new devloper onboarding" would be:
  - git clone github.com/some/software
  - docker compose up

### Using Compose to Build
* Will build the image with `docker compose up` if not found in cache
* Also rebuild with `docker compose build`

用 `docker compose down --rmi local` 把用完的image砍了
