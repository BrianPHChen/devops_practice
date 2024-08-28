### network

```bash
$ docker container run -d --name proxy -p 80:80 nginx

172.17.0.2

$ docker container inspect --format '{{.NetworkSettings.IPAddress}}' proxy

$ ifconfig
發現內部ip跟host ip不同

```

> docker network connect

用於attach network 到一個container (可以有多個network)
`disconnect` 用來斷線

### DNS

容器名的DNS只有在自定義網路中可以使用(建議都自定義，未來在compose時會更輕鬆使用)

```bash
$ docker network create my_net
$ docker container run -d --name my_nginx_name --network my_net nginx:alpine

$ docker container run -d --name my_nginx_name2 --network my_net nginx:alpine

$ docker container exec -it my_nginx_name ping my_nginx_name2
```