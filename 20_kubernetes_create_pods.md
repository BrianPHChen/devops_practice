### Create pods
* three ways to create pods
  * `kubectl run` (single pods command since 1.18)
  * `kubectl create` (create some resources via CLI or YAML)
  * `kubectl apply` (create/update anything via YAML)
* For now we'll just use `run` or `create` CLI
* Later we'll learn YAML and pros/cons of each

### Run
* Are we working?
  * `kubectl version`
* Two ways to deploy Pods (containers): Via commands, or via YAML
* Let's run a pod of the nginx web server!
  * `kubectl run my-nginx --image nginx`
* Let's list the pod
  * `kubectl get pods`
* Let's see all objects
  * `kubectl get all`

### Pods: Why do they exist
* Unlike Docker, you can't create a container directly in K8s
* You create Pod(s) (via CLI, YAML, or API)
  * Kuberetes then creates the container(s) inside it
* `kubelet` tells the container runtime to create containers for you
* Every type of resource to run containers uses Pods

### Creating a Deployment with kubectl
* Let's create a Deployment of the nginx web server!
  * `kubectl create deployment my-nginx --image nginx`
* Let's remove the single Pod and the Deployment
  * `kubectl delete pod my-nignx`
  * `kubectl delte deployment my-nginx`ss

### Scaling ReplicaSets
* Start a new deployment for one replica/pod
  * `kubectl create deployment my-apache --image httpd`
* Check our resource status
  * `kubectl get all`
* Let's scale it up with another pod
  * `kubectl scale deploy/my-apache --replica 2`
  * `kubectl scale deploy my-apache --replica 2`
  * those are the same command
  * deploy = deployment = deployments

### Inspacting Resources with Get
* List common resources
  * `kubectl get all`
* If missing my-apache, then recreate
  * `kubectl create deployment my-apache --image httpd --replicas 2`
* Show more with a wide output
  * `kubectl get all -o wide`
* Inspecting Resources with Describe
  * `kubectl describe deploy/my-apache`
* Watching Resources
  * On Linux, we might use a `watch kubectl get pods` command
  * But kubectl has `-w` (`--watch`) built-in!
  * `kubectl get pods -w`
  * `kubectl get events --watch-only`
* Container logs
  * Get a container's logs (picks a random replica, first container only)
    * `kubectl logs deploy/my-apache`
  * Follow new log entries, and start with the latest log line
    * `kubectl logs deploy/my-apache --follow --tail 1`
  * Get a specific container's logs in a pod
    * `kubectl logs pod/my-apache-xxx-yyy -c httpd`