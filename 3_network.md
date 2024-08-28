```bash
$ docker container run -d --name proxy -p 80:80 nginx

172.17.0.2

$ docker container inspect --format '{{.NetworkSettings.IPAddress}}' proxy

$ ifconfig
發現內部ip跟host ip不同

```