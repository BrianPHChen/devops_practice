### Registry

* Run the registry image
  * `$ docker container run -d -p 5000:5000 --name registry registry`
* Re-tag an existing image and push it to your new registry
  * `$ docker tag hello-world 127.0.0.1:5000/hello-world`
  * `$ docker push 127.0.0.1:5000/hello-world`
* Remove that image from local cache and pull it from new registry
  * `$ docker image remove hello-world`
  * `$ docker image remove 127.0.0.1:5000/hello-world`
  * `$ docker pull 127.0.0.1:5000/hello-world`
* Re-create registry using bind mount and see how it stores data
  * `$ docker container run -d -p 5000:5000 --name registry -v $(pwd)/registry-data:/var/lib/registry registry`


### On Swarm

* Works the same way as localhost
* Because of Routing Mesh, all nodes can see 127.0.0.1:5000
* Remember to decide how to store images (volume driver)
* NOTE: All nodes must be able to access images
* ProTip: Use a hosted SaaS registry if possible
