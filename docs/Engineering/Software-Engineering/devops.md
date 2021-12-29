# DevOps

[TOC]

# Cloud Platforms

## AWS

### AWS Cost Optimization
- https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/wellarchitected-cost-optimization-pillar.pdf
- https://www.cloudhealthtech.com/blog/10-aws-cost-optimization-best-practices

### IAM - Identity and Access Management

### Computing
#### AMI - Amazon Machine Image
#### Instance

### Storage
#### Bucket

### Database

### CI/CD

#### AWS Elastic Beanstalk
- Source: https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/Welcome.html

#### AWS CodeDeploy
AWS CodeDeploy is a deployment service that automates application deployments to Amazon EC2 instances, on-premises instances, or serverless Lambda functions.

- Source: https://docs.aws.amazon.com/codedeploy/latest/userguide/welcome.html

---
# CI/CD Tools

## Kubernet
## Ansible
## Jenkins
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

## `nginx`
## `gunicorn`
## Apache
## `ngrok`
## CloudFlare

---
# Load Balancer
- https://www.ateam-oracle.com/long-lived-tcp-connections-and-load-balancers
	- what happens when one or more servers comes up behind a load balancer?
		- what in case of long lived TCP conn?

## Algorithms
- https://blog.twitter.com/engineering/en_us/topics/infrastructure/2019/daperture-load-balancer.html

---
# Data Center/Computer Clusters Manager  /  container-orchestration system

## Tools

### Kubernetes

#### Minikube (Run Local)
- https://github.com/kubernetes/minikube

#### Load Balancer
- https://aws.amazon.com/blogs/opensource/network-load-balancer-nginx-ingress-controller-eks/
- https://cloud.google.com/kubernetes-engine/docs/tutorials/http-balancer

#### Long Lived Conn
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
```
