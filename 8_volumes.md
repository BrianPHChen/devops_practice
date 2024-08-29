### Volumes

> docker volume prune

先清除一下沒用的volume

> docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True mysql

執行mysql db

> docker inspect mysql

直接可以看到Mounts相關的資訊
```bash
前略
  "Mounts": [
      {
          "Type": "volume",
          "Name": "8eeb437f0c8f1b9cd204b15468ba42761e18528dd817401cf95d627c2dd1deb8",
          "Source": "/var/lib/docker/volumes/8eeb437f0c8f1b9cd204b15468ba42761e18528dd817401cf95d627c2dd1deb8/_data",
          "Destination": "/var/lib/mysql",
          "Driver": "local",
          "Mode": "",
          "RW": true,
          "Propagation": ""
      }
  ],
後略
```

### 停止並且刪除container，相依的volume不會被刪除

#### 1. 手動刪除所有的 volume
停止並且刪除container，相依的volume不會被刪除

`docker volume prune` 沒有辦法刪除所有的volume

* 停止並刪除所有的container
  ```bash
  $ docker stop $(docker ps -aq)
  $ docker rm $(docker ps -aq)
  ```
* 刪除所有的volume
  ```bash
  $ docker volume rm $(docker volume ls -q)
  ```

#### 2. Named Volumes
會更清楚volume在幹嘛
> docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True -v mysql-db:/var/lib/mysql mysql

### Create Docker
在run容器前先建立一個volume
> docker volume create

### Bind Mounting
* mount 一個host的file/dir給container的file/dir
* can't use in Dockerfil, must be at `container run`
* `run -v /Users/brian/stuff:/path/container` 要用full path name

> docker container run -d --name nginx -p 80:80 -v $(pwd):/usr/share/nginx/html nginx

### Postgres password
要在`docker run` 時設定env
`POSTGRES_PASSWORD=mypasswd` or `POSTGRES_HOST_AUTH_METHOD=trust` to ignore password
