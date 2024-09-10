### Exposing Containers
* `kubectl expose` creates a sevice for existing pods
* A sevice is a stable address for pod(s)
* If we want to connect to pod(s), we need a service
* CoreDNS allows us to resolve service by name
* There are different types of services
  * ClusterIP
  * NodePort
  * LoadBalancer
  * ExternalName

### Basic Service Types
* ClusterIP
  * Single, internal virtual IP allocated
  * Only reachable from within cluster (nodes and pods)
  * Pods can reach service on apps port number
* NodePort
  * High port allocated on each node
  * Port is open on every node's IP
  * Anyone can connect (if they can reach node)
  * Other pods need to be updated to this port
* These services are always available in Kubernetes

### More Service Types
* LoadBalancer
  * Controls a LB endpoint external to the cluster
  * Only available when infra provider gives you a LB (AWS ELB, etc)
  * Created NodePort+ClusterIP services, tells LB to send to NodePort
* External Name
  * Adds CNAME DNS record to CoreDNS only
  * name to use for something outside Kubernetes
* Kubernetes Ingress