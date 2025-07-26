# How to Install Kubernetes (Minikube) on Debian/Ubuntu

## 1. Install a Hypervisor

Minikube can run with several hypervisors. For this guide, we will use Docker. Make sure you have Docker installed first.

## 2. Install Minikube

Download the latest Minikube binary:

```bash
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

Make it executable and move it to your path:

```bash
chmod +x minikube
sudo mv minikube /usr/local/bin/
```

## 3. Install kubectl

`kubectl` is the command-line tool for interacting with a Kubernetes cluster. Download and install it:

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

## 4. Start Minikube

Now you can start a local Kubernetes cluster:

```bash
minikube start --driver=docker
```

## 5. Verify the Installation

Check the status of your cluster:

```bash
minikube status
```

And run a basic `kubectl` command:

```bash
kubectl get nodes
```
