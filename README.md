####This image and information below is based on https://github.com/anup1384/jenkins-k8s
###You can also read https://medium.com/faun/deploying-and-scaling-jenkins-on-kubernetes-2cd4164720bd
# Jenkins in Kubernetes
This repository has a `Dockerfile` and a `helm` chart for setting up a simple Jenkins master for running in Kubernetes.

This Jenkins has the required tools to work in and with Kubernetes
- Jenkins application with pre-loaded plugins (see [plugins.txt](plugins.txt))
- Skipped setup wizard
  - You can control admin user and password with `--set adminUser=${USER},adminPassword=${PASSWORD}`
  - You can add and remove plugins by editing the [plugins.txt](plugins.txt) file


### Build the Jenkins Docker image
You can build the image yourself
```bash
# Clone the image using git
$ git clone https://github.com/meirmichaeli/jenkins-k8s.git

# Build the image
$ docker build -t meirmichaeli/jenkins:v0.0.1 .

# Push the image
$ docker push meirmichaeli/jenkins:v0.0.1
```

### Deploy Jenkins helm chart to Kubernetes
```bash
# Init helm and tiller on your cluster
$ helm init
$ kubectl apply -f rbac-config.yaml

# Deploy the Jenkins helm chart
# (same command for install and upgrade)
$ helm upgrade --install jenkins ./helm/jenkins-k8s
```

### Data persistence
By default, in Kubernetes, the Jenkins deployment uses a persistent volume claim that is mounted to `/var/jenkins_home`.
This assures your data is saved across crashes, restarts and upgrades.   

