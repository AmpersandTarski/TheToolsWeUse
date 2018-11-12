---
description: >-
  (under construction) Deploying an Ampersand application in the cloud gives
  many benefits: continuous deployment, zero downtime, unlimited scalability.
  This is done on the Kubernetes platform.
---

# Deploying with Kubernetes

## Purpose

Deploying your Ampersand application to production can be done fast and frequent. For this purpose we are working on deployment on the Kubernetes platform. This allows you to deploy easily on your laptop \(for testing\), in your own data center \(The minimum you need is a virtual machiine that runs kubernetes\), or in the cloud \(to benefit from the reliability and security provided by hosting providers\). We use Kubernetes because it is open, free, well known, widely used, and is continuously being impoved by a large community. It lets you deploy fast and lets you upgrade the application without taking it offline.

## Way of working

1. You need a Kubernetes cluster, which you get from your provider, from your data center, or you create one yourself \(e.g. on your laptop\). A cluster is built on top of virtual or physical machines and hosts the services that expose \(i.e. to internet\).
2. On the platform I need a registry from which Kubernetes can pull the image\(s\).

I tried it out for myself. I stole my inspiration from [Kevin Smets' instruction](https://gist.github.com/kevin-smets/b91a34cea662d0c523968472a81788f7). Thank you Kevin! I ran the following from my terminal \(i.e. MacOS cli\)

### Requirements

To make a Kubernetes cluster, I used Minikube. Minikube requires that VT-x/AMD-v virtualization is enabled in BIOS. To check that this is enabled on OSX / macOS, I ran:

```text
sysctl -a | grep machdep.cpu.features | grep VMX
```

If there's output, it works!

### Prerequisites

* kubectl
* docker \(for Mac\)
* minikube
* virtualbox

```text
brew update && brew install kubectl && brew cask install docker minikube virtualbox
```

### Verify

```text
docker --version                # Docker version 17.09.0-ce, build afdb6d4
docker-compose --version        # docker-compose version 1.16.1, build 6d1ac21
docker-machine --version        # docker-machine version 0.12.2, build 9371605
minikube version                # minikube version: v0.22.3
kubectl version --client        # Client Version: version.Info{Major:"1", Minor:"8", GitVersion:"v1.8.1", GitCommit:"f38e43b221d08850172a9a4ea785a86a3ffa3b3a", GitTreeState:"clean", BuildDate:"2017-10-12T00:45:05Z", GoVersion:"go1.9.1", Compiler:"gc", Platform:"darwin/amd64"}      
```

### Start

```text
minikube start
```

This can take a while, expected output:

```text
Starting local Kubernetes cluster...
Kubectl is now configured to use the cluster.
```

Great! You now have a running Kubernetes cluster locally. Minikube started a virtual machine for you, and a Kubernetes cluster is now running in that VM.

### Check k8s

```text
kubectl get nodes
```

Should output something like:

```text
NAME       STATUS    ROLES     AGE       VERSION
minikube   Ready     <none>    40s       v1.7.5
```

Within minikube, a docker platform is running. However, on my Mac I have another docker daemon running. But  when we talk to docker, we definitely want to talk to the docker daemon that is inside minikube...

### Use minikube's built-in docker daemon

```text
eval $(minikube docker-env)
```

\(You might add this line to `.bash_profile` or `.zshrc` or ...  to use minikube's daemon by default. Or if you do not want to set this every time you open a new terminal\).

If I want to talk to the docker daemon on my Mac, I have to revert back to it by running:

```text
eval $(docker-machine env -u)
```

When running `docker ps`, it showed the following output:

```text
CONTAINER ID        IMAGE                                      COMMAND                  CREATED             STATUS              PORTS               NAMES
3835176d93bb        k8s.gcr.io/k8s-dns-sidecar-amd64           "/sidecar --v=2 --lo…"   30 minutes ago      Up 30 minutes                           k8s_sidecar_kube-dns-86f4d74b45-4b48w_kube-system_91346644-e424-11e8-bae2-080027501972_0
3c803544be8a        k8s.gcr.io/kubernetes-dashboard-amd64      "/dashboard --insecu…"   30 minutes ago      Up 30 minutes                           k8s_kubernetes-dashboard_kubernetes-dashboard-6f4cfc5d87-mvtgw_kube-system_962829f4-e424-11e8-bae2-080027501972_0
1d74c735c1df        k8s.gcr.io/coredns                         "/coredns -conf /etc…"   30 minutes ago      Up 30 minutes                           k8s_coredns_coredns-c4cffd6dc-xn62h_kube-system_961c845a-e424-11e8-bae2-080027501972_0
308bd132b35a        gcr.io/k8s-minikube/storage-provisioner    "/storage-provisioner"   31 minutes ago      Up 30 minutes                           k8s_storage-provisioner_storage-provisioner_kube-system_963bf651-e424-11e8-bae2-080027501972_0
```

The list was in fact a little bet longer: it contained 22 containers.

#### Build, deploy and run an image on your local k8s setup

First setup a local registry, so Kubernetes can pull the image\(s\) from there:

```text
docker run -d -p 5000:5000 --restart=always --name registry registry:2
```

### Build

First of, store all files \(Dockerfile, my-app.yml, index.html\) in this gist locally in some new \(empty\) directory.

You can build the Dockerfile below locally if you want to follow this guide to the letter. Store the Dockerfile locally, preferably in an empty directory and run:

```text
docker build . --tag my-app
```

You should now have an image named 'my-app' locally, check by using `docker images` \(or your own image of course\). You can then publish it to your local docker registry:

```text
docker tag my-app localhost:5000/my-app:0.1.0
```

Running `docker images` should now output the following:

```text
REPOSITORY                                             TAG                 IMAGE ID            CREATED             SIZE
my-app                                                 latest              cc949ad8c8d3        44 seconds ago      89.3MB
localhost:5000/my-app                                  0.1.0               cc949ad8c8d3        44 seconds ago      89.3MB
httpd                                                  2.4-alpine          fe26194c0b94        7 days ago          89.3MB
```

### Deploy and run

Store the file below `my-app.yml` on your system and run the following:

```text
kubectl create -f my-app.yml
```

You should now see your pod and your service:

```text
kubectl get all
```

The configuration exposes `my-app` outside of the cluster, you can get the address to access it by running:

```text
minikube service my-app --url
```

This should give an output like `http://192.168.99.100:30304` \(the port will most likely differ\). Go there with your favorite browser, you should see "Hello world!". You just accessed your application from outside of your local Kubernetes cluster!

### Kubernetes GUI

```text
minikube dashboard
```

### Delete deployment of my-app

```text
kubectl delete deploy my-app
kubectl delete service my-app
```

You're now good to go and deploy other images!

## Reset everything

```text
minikube stop;
minikube delete;
rm -rf ~/.minikube .kube;
brew uninstall kubectl;
brew cask uninstall docker virtualbox minikube;
```

### Version

Last tested on 2017 October 20th macOS Sierra 10.12.6

