### Basic Terms

* Kubernetes: The whole orchestration system
  * K8s "k-eights" or Kube for short
* Kubectl: CLI to configure Kubernetes and manages apps
  * Using "cube control" official pronunciation
* Node: Single server in the Kubernetes cluster
* Kubelet: Kubernetes agent running on nodes
* Control Plane: Set of containers that manage the cluster
  * Includes API server, scheduler, controller manager, etcd, and more
  * Somtimes called the "master"

### Install Kubernetes Locally
* Kuberbetes is a series of containers, CLI's and configurations
* Many way to install, lets focus on easiet for learning
* Docker Desktop: Enable in settings
  * Sets up everthing inside Docker's existing Linux VM
* Docker Toolbox on Windows: MiniKube
  * Uses VirtualBox to make Linux VM
* Your Own Linux Host or VM: MicroK8s
  * Install Kubernetes right on the OS

### Kubernetes In a Browser
* Try http://play-with-k8s.com or katacoda.com in browser
  * Easy to get started
  * Doesn't keep your environent

### Docker Desktop
* Runs/configures Kubernetes Master containers
* Manages kubectl install and certs
* Easily install, disable, and remove from Docker GUI

### MiniKube
* Download Windows Installer from Github
* minikube-installer.exe
* minikube start
* Much like the docker-machine experience
* Creates a VirtualBox VM with Kubernetes master setup
* Doesn't install kubectl

### MicroK8s
* Install Kubernetes (without Docker Engine) on localhost(Linux)
* Uses snap (rather then apt or yum) for install
* Control the MicroK8s service via `microk8s`. commands
* kubectl accessable via microk8s.kubectl
* Add an alias to your shell (.bash_profile)
  * `alias kubectl=microk8s.kubectl`

### Kubernetes Container Abstractions
* Pod: one or more containers running together on one Node
  * Basic unit of deployment. Containers are always in pods
* Controller: For creating/updating pods and other objects
  * Many types of Controllers inc. Deployment, ReplicaSet, StatefulSet, DaemonSet, Job, CronJob, etc.
* Service: network endpoint to connect to Pod
* Namespace: Filtered group of objects in cluster
* Secrets, ConfigMaps, and more