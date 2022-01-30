# devops-kubernetes-nomuerasenelinteto-p3
https://www.youtube.com/watch?v=16Nqs8Uo1Ck


## Instalación de kubernetes -  Creando la maquina virtual

## Instalación de kubernetes -  Modificando configuraciones
* 2cores 
* 2GB RAM 
* 30GB DD
* Cambiar el tipo del adaptador a bridge

## Instalación de kubernetes -  Seleccionando el ubuntu
## Instalación de kubernetes -  Iniciando la maquina virtual
## Instalación de kubernetes -  Configurando el ubuntu
## Instalación de kubernetes -  Iniciando la instalación del ubuntu
## Instalación de kubernetes -  Explicacion modelo de responsabilidad compartida con las nubes
## Instalación de kubernetes -  El ubuntu despues de la instalación

## Instalación de kubernetes -  Instalación de Docker
* https://docs.docker.com/engine/install/ubuntu/
* Agregar el usuario creado al grupo de Docker

## Instalación de kubernetes -  Instalación de minikube
* https://minikube.sigs.k8s.io/docs/start/
* *  Descomprimir el archivo en ```$HOME/use_programs```
* ```bash
    export PATH=$HOME/use_programs:$PATH 
  ```

## Iniciando el cluster con Docker
* ```bash
    minikube start
  ```
## Verificando el container runtime del cluster
* ```bash
    minikube kubectl --  describe pod kube-scheduler-minikube -n kube-system |grep “Container ID”
  ``` 
## Deteniendo el cluster 
* ```bash
    minikube stop
  ```
## Iniciando el cluster con containerd
* ```bash
    minikube start --container-runtime containerd
  ```
## Verificando el container runtime del cluster
* ```bash
    minikube kubectl --  describe pod kube-scheduler-minikube -n kube-system |grep “Container ID”
  ``` 