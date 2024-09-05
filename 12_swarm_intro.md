### Swarm
* Swarm Mode is a clustering solution built inside Docker
* Not related to Swarm 'classic' for pre=1.12 versions
* Added in 1.12 (Summer 2016) via SwarmKit toolkit
* Enhanced in 1.13 (January 2017) via Stacks and Secrets
* Not enable by default, new commands once enabled
  * docker swarm
  * docker node
  * docker service
  * docker stack
  * docker secret

### Single Node Swarm

> $ docker swarm init

What just happened?
* Lots of PKI and security automation
  * Root Signing Certificate created for our Swarm
  * Certificate is issued for first Manager node
  * Join tokens are created
* Raft database created to store root CA, configs and secrets

> docker node ls

看到single node的資訊

> $ docker service create alpine ping 8.8.8.8

> $ docker service ls

```
ID             NAME            MODE         REPLICAS   IMAGE           PORTS
nlu7414wt4bk   great_mcnulty   replicated   1/1        alpine:latest  
```

> $ docker service ps great_mcnulty

```
ID             NAME              IMAGE           NODE             DESIRED STATE   CURRENT STATE                ERROR     PORTS
r6siv3to0xgq   great_mcnulty.1   alpine:latest   docker-desktop   Running         Running about a minute ago  
```

> $ docker container ls

```
CONTAINER ID   IMAGE           COMMAND          CREATED         STATUS         PORTS     NAMES
83f721db04b2   alpine:latest   "ping 8.8.8.8"   2 minutes ago   Up 2 minutes             great_mcnulty.1.r6siv3to0xgqtr097j8gctfek
```

> $ docker service update nlu7414wt4bk --replicas 3

> $ docker service ls

```
ID             NAME            MODE         REPLICAS   IMAGE           PORTS
nlu7414wt4bk   great_mcnulty   replicated   3/3        alpine:latest   
```

> $ docker service ps great_mcnulty

```
ID             NAME              IMAGE           NODE             DESIRED STATE   CURRENT STATE                ERROR     PORTS
r6siv3to0xgq   great_mcnulty.1   alpine:latest   docker-desktop   Running         Running 6 minutes ago                  
yjjoae4hxp7c   great_mcnulty.2   alpine:latest   docker-desktop   Running         Running about a minute ago             
xb5zpu5o7ml5   great_mcnulty.3   alpine:latest   docker-desktop   Running         Running about a minute ago 
```

> $ docker container ls

```
CONTAINER ID   IMAGE           COMMAND          CREATED         STATUS         PORTS     NAMES
2aee22ea4ba7   alpine:latest   "ping 8.8.8.8"   4 minutes ago   Up 4 minutes             great_mcnulty.3.xb5zpu5o7ml5ygfm6zjbh16v0
0061962efee5   alpine:latest   "ping 8.8.8.8"   4 minutes ago   Up 4 minutes             great_mcnulty.2.yjjoae4hxp7c5dr60ikuu2psi
83f721db04b2   alpine:latest   "ping 8.8.8.8"   8 minutes ago   Up 8 minutes             great_mcnulty.1.r6siv3to0xgqtr097j8gctfek
```

> $ docker container rm -f great_mcnulty.1.r6siv3to0xgqtr097j8gctfek

他會被砍掉一個
```
ID             NAME            MODE         REPLICAS   IMAGE           PORTS
nlu7414wt4bk   great_mcnulty   replicated   2/3        alpine:latest 
```
然後在快速長回來

> $ docker service ps nlu7414wt4bk

```
ID             NAME                  IMAGE           NODE             DESIRED STATE   CURRENT STATE                ERROR                         PORTS
vwwsxqqn80lk   great_mcnulty.1       alpine:latest   docker-desktop   Running         Running about a minute ago                                 
r6siv3to0xgq    \_ great_mcnulty.1   alpine:latest   docker-desktop   Shutdown        Failed about a minute ago    "task: non-zero exit (137)"   
yjjoae4hxp7c   great_mcnulty.2       alpine:latest   docker-desktop   Running         Running 6 minutes ago                                      
xb5zpu5o7ml5   great_mcnulty.3       alpine:latest   docker-desktop   Running         Running 6 minutes ago   
```
可以看到被砍掉的歷史紀錄

真的要砍掉service
> $ docker service rm great_mcnulty

使用這個指令關閉swarm
> $ docker swarm leave --force

### Create 3-Node Swarm
* play-with-docker.com
  * Only needs a browser, but resets after 4 hours
* docker-machine + virtualbox (現在已建議使用multipass，而不用docker-machine)
  * free and runs locally, but requires a machine with 8GB memory
* digital ocean + docker install
  * most like a production setup, but costs $5-10/node/month while learning
  * install docker anywhere with get.docker.com

### Overlay Multi-Host Networking
* `--driver overlay` when createing network
* For container-to-container traffic inside a single Swarm
* Each service can be connected to multiple networks

> $ docker network create --driver overlay mydrupal

> $ docker service create --name psql --network mydrupal -e POSTGRES_PASSWORD=mypass postgres

開另一個服務

> $ docker service create --name drupal --network mydrupal -p 80:80 drupal

內部自己做loadbalancer, 不論服務在哪個node

> $ docker service create --name search --replicas 3 -p 9200:9200 elasticsearch:2

> $ curl localhost:9200

每次名稱可能不一樣

* Routing Mesh
  * This is stateless load balancing

### Swarm Stacks
* Stacks: Production Grade Compose
* `docker stack deploy`
* 用 `deploy` in compose file, can't do `build`
* Compose ignores `deploy`, swarm ignores `build`
* `docker-compose` cli not needed on Swarm server

### Secrets Storage
* Easiest "secure" solution for storing secrets in Swarm
* Only stored on disk on Manager nodes
* Secrets are first stored in Swarm, then assigned to a Service
* only container in assigned service can see them
* looks like files but are actually in-memory fs
* /run/secrets/<secret_name> or /run/secrets/<secret_alias>
* Local docker-compose can use file-based secrets, but not secure

Go to `secrets-sample-2` Assignement

> $ docker stack deploy -c docker-compose.yml mydb

> $ docker stack rm mydb 

如果想要換密碼rm secret 就會需要重啟services
使用檔案的話建議更新進去swarm讓他管理之後就把檔案刪掉