# What is this
This is a self tested way to deploy nginx, busybox and wordpress to local k8s environment

# Prerequisite
A kubernetes environment and kubectl command is available locally to access the k8s cluster

# My mac k8s environment steps
And of course, you can rent a gcp or aws for an k8s environment. Or else, you can use VirtualBox or Vmware to start a local linux and install k8s step by step. But now for MAC the easist way is to install docker for mac and use it to install k8s with one mouse button click. Here are the steps.
1. I downloaded from here for my MacBook
https://www.docker.com/products/docker-desktop
2. After registering user/password, click the docker whael button in mission slot and choose preference.
3. Then Kubernetes tab
4. Enable Kubernetes, choose Kubernetes(not Swarm), click show system pods if you wish
5. Wait for installation
6. Done

# How to play

### busybox.yaml
Use this command to create a busybox(no service)
```
kubectl create -f busybox.yaml
```

### nginx.yaml
Use this command to create a nginx(with nodeport service)
```
kubectl create -f nginx.yaml
```

### ubuntu.yaml
Same way to create this so you can have ability to do some hacking by using
```
kubectl exec -it [ubuntu pod name] /bin/bash
```

### latest-wp.zip
Latest wordpress php package download from here https://wordpress.org/download/

### wordpress/docker-build/
Here we have a Dockerfile. Use the command to build a docker image, at default, name it **buddy/wordpress:latest**
```
docker build -t buddy/wordpress:latest . 
```

### Build Wordpress
Based on previous step, run in sequence
```
#create the volumn
kubectl create -f v.yaml

#create mysql
kubectl create -f mysql.yaml

#create wordpress deployment and service
kubectl create -f wp.yaml
```
