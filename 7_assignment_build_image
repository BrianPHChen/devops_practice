### Assignment
* Dockerfiles are part process workflow and part art
* Take existing Node.js app and Dockerize it
* Make `Dockerfile`. Build it. Test it. Push it.(rm it). Run it.
* Expect this to be iterative. Rarely do I get it right the first time.
* Use the Alpine version of the official 'node' 6.x image
* Expected result is web site at http://localhost
* Tag and push to your Docker Hub account
* Remove your image from local cache, run again from hub

### Answer
[assignement](https://github.com/BrianPHChen/udemy-docker-mastery/tree/main/dockerfile-assignment-1)

```dockerfile
FROM node:6-alpine
EXPOSE 3000
RUN apk add --update tini
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
COPY package.json packate.json
RUN npm install && npm cache clean
COPY . .
CMD ["tini", "--", "node", "./bin/www"]
```
> docker build -t testnode .

> docker container run --rm -p 80:3000 testnode

接著做tag, push 這邊就不做了
