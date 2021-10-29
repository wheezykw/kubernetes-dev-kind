# kubernetes-dev-kind

## Introduction
  This guide will document steps to get up and running with Kubernetes in Development (KinD).
  
## Initial Setup
  1. Create Ubuntu VM
  2. Install and Configure Docker
  3. Install kind
      If you have Go installed use `go get sigs.k8s.io/kind`,
        or download the compiled binaries from https://github.com/kubernetes-sigs/kind
        and place them at `/usr/local/bin` to access them from anywhere in terminal.
  
## Getting Started
  1. `docker ps` will verify that Docker is working properly and no machines are running
  2. `cat ~/.kube/confg` will show that the kubernetes config file doesn't exist
  3. `kind create cluster` will create new cluster with one node
        If you want to create a multi node cluster. You can use a config.yaml file in the root of the project:
          1. Create a project folder
          2. Create a file called config.yaml
          3. Follow the example in the config.yaml file
          4. `kind create cluster --config=config.yaml` This will start kind based on the configuration from the external file.
        Note: Every node created in kind is a container not a virtual machine.
  4. At this point, kind is running and you can run any kubectl commands.
          1. `kubectl get nodes` You may need to wait a few seconds to let the nodes start up. They will say Ready under STATUS when they are ready to go.
          2. `docker ps` will show you the `kind-control-plane` and `kind-worker` nodes running showing that kind is running in Docker instead of a VM.

## Working with Control Plane Container
  1. `docker ps` will show you the Docker containers and their details
  2. `docker exec -it <container-id> sh` You will need to copy the container id from the control plane that is the output of the previous command. This will give you a shell within the control plane.
  3. `ls /etc/kubernetes` This will show the Kubernetes configuration files in the control plane.
  4. `exit` will let you exit from the shell of the master node
