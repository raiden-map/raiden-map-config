# Build Raiden Map for development

## What is Raiden Map?

## Why build Raiden Map for development?

## Last Update


## Getting started

1. **Running up local K8s**
2. **Create Raiden Map Kafka cluster and MySQL**
2. **Dockerize Raiden Map components**
3. **Create Raiden Map pods**

### Installation
1. **Running up local K8s**:
* Linux:
    * First of all install Docker-CE: I'm using Ubuntu distro but it's the same with the others. So, you go to [installation page](https://docs.docker.com/install/linux/docker-ce/ubuntu) and follow one of the guide ( repository or package installation). Then make sure than Docker has root-permission and if you want that it starts on boot so follow [this](https://docs.docker.com/install/linux/linux-postinstall/). I reccomend to configure your terminal for the [command-line completion](https://docs.docker.com/compose/completion/).
    * Install [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/). You are now installed:
        1. kubectl ( I reccomend also here to configure [auto-completion](https://kubernetes.io/docs/tasks/tools/install-kubectl/#optional-kubectl-configurations));
        2. hypervisor ( I use VirtualBox )
        2. minikube
    * Start minikube:
        I'm using this VM config:
        ```bash 
        minikube start --disk-size 50000MB --cpus 4 --memory 4096 
        ```
        you can set other parameters, see them with:
        ```bash
        minikube start -h
        ```
        Wait for minikube to be ready!

2. **Create Raiden Map Kafka cluster and MySQL**:

    For this point you can also read pdf in **Configuration-guide** folder.

    **Remember**: At every terminal opened you must set docker-env for minikube:

    ```bash
    eval $(minikube docker-env)
    ``` 
3. **Dockerize Raiden Map components**:

    Open terminal in folder that contains _Dockerfile_ ( you can do 
    <kbd>SHIFT</kbd>+<kbd>F10</kbd> and then <kbd>E</kbd> ) then build the container:
    ```bash
    docker build -t image_name:image_version .
    ```
    you can find name and version in .yaml file of the component: 
    ```yaml
    spec: 
        containers: 
            image: image_name:image_version
    ```
    The first time it takes a few minutes to download all the requirements.

    
4. **Create Raiden Map pods**:

   Now the last one, go to the folder that contains the .yaml file and run:

    ```bash
    kubectl create -f my-component.yaml --namespace my-namespace
    ```

   if all ok you can see all the pods that are running with:

   ```bash
    kubectl get pods --namespace my-namespace
    ```
    and see the logs:
    ```bash
    kubectl logs -f my-pod --namespace my-namespace
    ```








