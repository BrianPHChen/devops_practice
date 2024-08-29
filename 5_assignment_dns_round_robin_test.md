### Assignment
* Ever since Docker Engine 1.11, we can have multiple containers on a created network respond to the same DNS address
* Create a new virtual network (default bridge driver)
* Created 2 containers from `elasticsearch:2` image
* Research and use `-network-alias search` when creating them to give them an additional DNS name to respond to
* Run `alpone nslookup search` with `--net` to see the two containers list for the same DNS name
* Run `centos curl -s search:9200` with `--net` multiple times until you see both "name" fiedls show

### Answer

> docker network create my_net

> docker container run -d --net my_net --net-alias httpenv bretfisher/httpenv
連續做兩次

> docker container run --rm --net my_net alpine nslookup httpenv
```
Server:		127.0.0.11
Address:	127.0.0.11:53

Non-authoritative answer:
Name:	httpenv
Address: 172.18.0.3
Name:	httpenv
Address: 172.18.0.2
```
> docker container run --rm --net my_net centos curl -s httpenv:8888

```
> docker container run --rm --net my_net centos curl -s httpenv:8888
{"HOME":"/root","HOSTNAME":"b49b3503a7a9","PATH":"/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"}%
> docker container run --rm --net my_net centos curl -s httpenv:8888
{"HOME":"/root","HOSTNAME":"3c32ed10497a","PATH":"/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"}%  
```
Hostname兩次不一樣