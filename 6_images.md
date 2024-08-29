### image
> docker pull nginx:latest

tag 為一種識別名稱 有可能會有alias

> docker image ls

> docker history nginx:latest

show 出這個image layer

> docker image inspect nginx:latest

這個image的所有設定

### Docker Hub

> docker login

登入docker hub (default)

> docker push "image"

push image

### Build Image
[sample dockerfile](https://github.com/BrianPHChen/udemy-docker-mastery/blob/main/dockerfile-sample-1/Dockerfile)

> docker image build -t customnginx .

build image

把可能會改變的命令往後寫 比較固定的命令放在前面 build起來比較快

[sample dockerfile 2](https://github.com/BrianPHChen/udemy-docker-mastery/tree/main/dockerfile-sample-2)

用official的nginx image但換掉html

`WORKDIR` 是類似cd的存在，可能會在執行不同命令時時常變換

