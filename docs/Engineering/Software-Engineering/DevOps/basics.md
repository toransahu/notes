# Basics

[TOC]

---
# Concepts/Principles

1. Automation – Reducing manual effort in deployments and monitoring.
1. Security – Ensuring systems are protected against threats (DevSecOps).
1. Performance – Optimizing speed and resource usage.
1. Resilience – Recovering quickly from failures.
1. Efficiency – Optimizing processes to minimize waste.
1. Compliance – Meeting regulatory and security requirements.
1. Collaboration – Enhancing teamwork between Dev and Ops.
---
1. Reliability – Ensuring systems are robust and fault-tolerant.
1. Scalability – Ability to handle increased workloads efficiently.
1. Observability – Gaining insights into system performance and issues.
1. Availability – Keeping services up and running with minimal downtime.
1. Maintainability – Ease of managing and updating infrastructure/code.
1. Flexibility – Adapting to changing requirements and environments.
1. Agility – Speed and adaptability in software development and deployment.
1. Portability – Moving applications easily across environments.
1. Usability – Ensuring tools and processes are developer-friendly.

---

# CI/CD

CI/CD offers:

1. Agility – CI/CD enables rapid iteration, quick feedback loops, and faster time to market.
1. Maintainability – Automates testing and deployment, making code easier to manage.
1. Reliability – Ensures consistent, tested, and error-free releases.
1. Scalability – Helps handle increasing workloads by automating deployments across environments.

## CircleCI
## Travis CI
## Github Actions
## Ansible

NOTE:

1. In a task
    1. during the loop: Keys like `rc`, `stdout`, etc., are available in the registered variable for the current iteration. For each loop iteration, Ansible executes the task and temporarily populates the registered variable (e.g., command_result) with the details of that specific run. changed_when is evaluated per iteration. The registered variable (command_result) contains the current iteration's details.

    1. After the loop: These keys are no longer present at the root level. All per-iteration details are stored in the results list. To work with individual results (like rc), you must access them from the results field. The changed status for the entire task is true if changed_when was true for any iteration.

## Jenkins

Pipeline as Code: JJB

## Chef
## Puppet

---
# Containers & VM

## Docker

Image, Repo, Tag naming convention

```bash
# BUILD an image & tag it - from Dockerfile in "." (current dir)
# semantics:
# docker build -t <tag>
# docker build -t <namespace>/<image|repo name>:<tag> .
$ docker build -t <target name>:[<tag>] .
# where target name is called image or repo name

# TAG an image
# semantics:
# docker tag <source>[:<tag>] <target>[:<tag>]
# docker tag <img ID|existing tag> <reposotiry>:<tag>
# docker tag <image> <namespace>/<repo name>:<tag>
$ docker tag <source>[:<tag>] <target>[:<tag>]
```

- tag: is a pointer to an image
	- are alias (e.g. my_image:latest, my_image:v1) to the image IDs (f1477ec11d12)
	- think of how diff. git tags can refer to a commit SHA
- image: is identified by an ID (hash/msg digest) of configs/layers (check if for same 2 config/Dockerfile if the ID is same)
	- each image can have 0 or more tags 
- repo: is an remote location under a namespace (i.e. account/username) where image(s?) are stored
- `:latest` is not always LATEST tag
	- https://blog.container-solutions.com/docker-latest-confusion

- https://stackoverflow.com/questions/44500367/when-would-a-docker-image-and-its-repository-have-different-names

## Vagrant

---
# Servers

## nginx
## gunicorn
## ngrok
## Apache Tomcat
## CloudFlare

---
# Proxy Server

---
# Reverse Proxy Server

---
# Load Balancer
- https://www.ateam-oracle.com/long-lived-tcp-connections-and-load-balancers
	- what happens when one or more servers comes up behind a load balancer?
		- what in case of long lived TCP conn?

## Algorithms
- https://blog.twitter.com/engineering/en_us/topics/infrastructure/2019/daperture-load-balancer.html

---
# Cluster Management & Orchestration

(Data center, cluster manager, container-orchestration system)

## Minikube (Run Local)
- https://github.com/kubernetes/minikube
- https://minikube.sigs.k8s.io/docs/start/

### Prerequisites

### Installation

```bash
$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

### Start Cluster

```bash
$ minikube start
```

### Explore Cluster

Get all the pods

```bash
$ minikube kubectl -- get pods -A

# or

$ alias kubectl='minikube kubectl --'
$ kubectl get pods -A
```

### Deploy Applications

```bash
# create deployment
$ minikube kubectl -- create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.4
# expose the port 8080 of the container
$ minikube kubectl -- expose deployment hello-minikube --type=NodePort --port=8080
# show hello-minikube service
$ minikube kubectl -- get services hello-minikube
# open the service in browser
# via option a)
$ minikube service hello-minikube
# or, via option b)
$ minikube kubectl -- port-forward service/hello-minikube 7080:8080  # open localhost:7080
```

#### `LoadBalancer` deployment

- the standard way to expose application to internet
- each service gets its own IP

```bash
# create a load-balanced deployment
$ minikube kubectl -- create deployment balanced --image=k8s.gcr.io/echoserver:1.4
# expose the server over port 8080
$ minikube kubectl -- expose deployment balanced --type=LoadBalancer --port=8080
# now create a tunnel in diff. window
$ minikube tunnel
# now show info of the service & open the <EXTERNAL-IP>:8080 to access
$ minikube kubectl -- get services balanced
```

### Manager cluster

```bash
# Upgrade your cluster:
$ minikube start --kubernetes-version=latest

# Pause Kubernetes without impacting deployed applications:
$ minikube pause

# Unpause a paused instance:
$ minikube unpause

# Halt the cluster:
$ minikube stop

# Increase the default memory limit (requires a restart):
$ minikube config set memory 16384

# Restart
$ minikube stop && minikube start

# Browse the catalog of easily installed Kubernetes services:
$ minikube addons list

# Enable an addon
$ minikube addons enable <name>

# Enable addon at startup
$ minikube start --addons <name1> --addons <name2>

# Open addon server in browser (iff)
$ minikube addons open <name>

# Disable an addon
$ minikube addons disable <name>

# Start a second local cluster
$ minikube start -p cluster2

# Create a second cluster running an older Kubernetes release:
$ minikube start -p aged --kubernetes-version=v1.16.1

# Delete the local cluster
$ minikube delete

# Delete all of the minikube clusters:
$ minikube delete --all
```

### Access application

More ways: https://minikube.sigs.k8s.io/docs/handbook/accessing/


### More

https://minikube.sigs.k8s.io/docs/handbook/

## Kubernetes (k8s)

### Pod
- A Kubernetes Pod is a group of one or more Containers, tied together for the purposes of administration and networking.

### Deployment
- A Kubernetes Deployment checks on the health of your Pod and restarts the Pod's Container if it terminates
- Deployments are the recommended way to manage the creation and scaling of Pods

### Service
By default, the Pod is only accessible by its internal IP address within the Kubernetes cluster. To make the hello-node Container accessible from outside the Kubernetes virtual network, you have to expose the Pod as a Kubernetes Service.

An abstract way to expose an application running on a set of Pods as a network service.

With Kubernetes you don't need to modify your application to use an unfamiliar service discovery mechanism. Kubernetes gives Pods their own IP addresses and a single DNS name for a set of Pods, and can load-balance across them.

### ReplicaSet

A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.

### Secrets

A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in a container image. Using a Secret means that you don't need to include confidential data in your application code.

### ConfigMaps

A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.

A ConfigMap allows you to decouple environment-specific configuration from your container images, so that your applications are easily portable.

### Ingress


### Namespace


### Job

### Start Cluster

tbd

### Addons

#### SealedSecret

https://github.com/bitnami-labs/sealed-secrets

#### k8s Load Balancer
- https://aws.amazon.com/blogs/opensource/network-load-balancer-nginx-ingress-controller-eks/
- https://cloud.google.com/kubernetes-engine/docs/tutorials/http-balancer

#### k8s Long Lived Conn
- Issue
	- https://learnk8s.io/kubernetes-long-lived-connections
	- https://tech.xing.com/a-reason-for-unexplained-connection-timeouts-on-kubernetes-docker-abd041cf7e02
	- https://kubernetes.io/blog/2019/03/29/kube-proxy-subtleties-debugging-an-intermittent-connection-reset/
	- https://www.edureka.co/community/57404/set-up-a-websocket-in-google-kubernetes-engine
- Sol
	- https://medium.com/johnjjung/how-to-use-gcp-loadbalancer-with-websockets-on-kubernetes-using-services-ingresses-and-backend-16a5565e4702


### Docker Swarm
### Docker Compose
### Apache Mesos

---
# Infrastructure as Code

## Terraform

https://www.terraform.io/

---
# Queues

## RabbitMQ
## Celery
## Redis
- Source: https://logz.io/blog/kafka-vs-redis/

## Apache Kafka
- a distributed streaming platform/framework
- Source: https://logz.io/blog/kafka-vs-redis/
- Use Case
    - building realtime data pipelines and streaming applications
    - messaging application

---

# ELK Stack
## Elasticsearch
- a no-sql db

## Logstash
- a log pipeline tool

## Kibana
- a vizualization tool


---

# Others




---
# Documentation Tool

## Sphinx
### ReadTheDoc
### MkDocs

## GitBook
## MoinMoin 

---
# Ref
1. https://www.znetlive.com/blog/compare-top-devops-tools-docker-kubernetes-puppet-chef-ansible/
