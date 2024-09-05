### Update

> $ docker service scale web=5 

* 用來增加服務

> $ docker service update --image nginx:1.13.6 web

* 用來改變image

> $ docker service update --publish-rm 8088 --publish-add 9090:80

* 修改port

> $ docker service update --force web

* 強制重開，可能會讓node上面的container重新分配到別的node上

> $ docker service rm web

* 刪除