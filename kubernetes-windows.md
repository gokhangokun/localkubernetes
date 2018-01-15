This Guide for Windows Users

# Requirements

Minikube requires that VT-x/AMD-v virtualization is enabled in BIOS.

# Prerequisites

- kubectl
- docker (for Mac)
- minikube
- virtualbox

**Install Chocolatey for Windows**

First, you’ll need the some configuration on PowerShell

Open PowerShell As **administration**  and run this command

```
Get-ExecutionPolicy
```

If it returns Restricted, then run and Type A for yes for all

```
Set-ExecutionPolicy AllSigned
```

Now run the following command on powershell

```
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```


Install Kubectl with Chocolatey

```
choco install kubernetes-cli
```

Install Virtualbox

```
choco install virtualbox
```

Install Docker

```
choco install docker
```


Install Docker Toolbox

```
choco install docker-toolbox
```

# Verify

    docker --version                # Docker version xx.xx.x-ce, build xxxxxx
    docker-compose --version        # docker-compose version x.xx.x, build xxxxxxx
    docker-machine --version        # docker-machine version x.xx.x, build xxxxxxx


Create Local Development Machine for Docker

```
docker-machine create --driver virtualbox dev
```
**If getting error like Error with pre-create check: "This computer is running Hyper-V. VirtualBox won't boot a 64bits VM when Hyper-V is activated. Either use Hyper-V as a driver, or disable the Hyper-V hypervisor. (To skip this check, use --virtualbox-no-vtx-check)"**

```
docker-machine create --driver hyperv dev
```

Install Minikube

```
choco install minikube
```

# Verify
    minikube version                # minikube version: vx.xx.x
    kubectl version --client        # Client Version: version.Info{Major:"1", Minor:"8", GitVersion:"v1.8.1", GitCommit:"xxxxxxxxxxxxxxxxxx", GitTreeState:"clean", BuildDate:"2017-12-12T02:45:25Z", GoVersion:"go1.9.1", Compiler:"gc", Platform:"darwin/amd64"}      
    
# Start

    minikube start
    
This can take a while, expected output:

    Starting local Kubernetes cluster...
    Kubectl is now configured to use the cluster.

You now have a running Kubernetes cluster locally.
Minikube started a virtual machine for you, and a Kubernetes cluster is now running in that VM.

# Check kubernetes

    kubectl get nodes
    
Should output something like:

    NAME       STATUS    ROLES     AGE       VERSION
    minikube   Ready     <none>    40s       vx.x.x
    
# Run Kubernetes GUI

    minikube dashboard
    
# Delete deployment of my-app

    kubectl delete deploy my-app
    kubectl delete service my-app
    
You're now good to go and deploy other images!

# Reset everything

    minikube stop;
    minikube delete;
    rm -rf ~/.minikube .kube;
    brew uninstall kubectl;
    brew cask uninstall docker virtualbox minikube;
