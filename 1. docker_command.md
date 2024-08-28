# Docker Command

> docker info

所有現在Docker Engine相關資訊

> docker container run --publish 80:80 nginx

執行一台nginx在前台，如果80 port被用了，也可以寫成`8080:80` or `8888:80` 把實體port寫在左邊mapping

> docker container run --publish 80:80 --detach nginx

執行一樣的服務加上`--detach`放到後台，接著會拿到container id

> docker stop <container id/name>

停止服務/容器

> docker container ls

顯示所有容器

### run vs. start
`docker container run` always重啟一個新容器

`docker container start` 啟動一個已經存在但是stopped的容器

> docker container logs <container id/name>

顯示logs

`docker container rm <container id/name>` 刪除容器也可以加上`-f` 強制刪除還在跑的 



