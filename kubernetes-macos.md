This Guide for MacOS Users

# Requirements

Minikube requires that VT-x/AMD-v virtualization is enabled in BIOS.

You can check your computer status with : 
    sysctl -a | grep machdep.cpu.features | grep VMX

If give you any output no problem, If not, enable VT-x/AMD-v on BIOS.

# Prerequisites

- kubectl
- docker (for Mac)
- minikube
- virtualbox

Install Homebrew for MacOS

First, you’ll need the command-line tools for Xcode installed.

In Terminal run this command

```
xcode-select --install
```

After, install Homebrew and Homebrew Cask

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Run the following command once you’re done to ensure Homebrew is installed and working properly:

```
brew doctor
```

If it is correctly install run this command for install hombrew cask

```
brew install caskroom/cask/brew-cask
```

Install Kubectl with Homebrew

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/darwin/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```

Install Virtualbox

```
brew cask install virtualbox
```

Install Docker

```
brew cask install docker
```


Install Docker Toolbox

```
brew cask install dockertoolbox
```

# Verify

    docker --version                # Docker version xx.xx.x-ce, build xxxxxx
    docker-compose --version        # docker-compose version x.xx.x, build xxxxxxx
    docker-machine --version        # docker-machine version x.xx.x, build xxxxxxx


Create Local Development Machine for Docker

```
docker-machine create --driver virtualbox default
```

Install Minikube

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.24.1/minikube-darwin-amd64
chmod +x minikube
sudo mv minikube /usr/local/bin/
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
    
# Use minikube's built-in docker daemon:

    eval $(minikube docker-env)
    
Running `docker ps` should now output something like:

```
CONTAINER ID        IMAGE                                         COMMAND                 CREATED             STATUS              PORTS               NAMES
8c0c1d69b9a1        gcr.io/google-containers/kube-addon-manager   "/opt/kube-addons.sh"   22 seconds ago      Up 22 seconds                           k8s_kube-addon-manager_kube-addon-manager-minikube_kube-system_c654b2f084cf26941c334a2c3d6db53d_0
5751dcb14adf        gcr.io/google_containers/pause-amd64:3.0      "/pause"                33 seconds ago      Up 33 seconds                           k8s_POD_kube-addon-manager-minikube_kube-system_c654b2f084cf26941c334a2c3d6db53d_0
```
    
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
