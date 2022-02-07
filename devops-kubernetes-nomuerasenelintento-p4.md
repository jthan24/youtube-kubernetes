# devops-kubernetes-nomuerasenelinteto-p4
https://www.youtube.com/watch?v=CpBta3ZLaH4


## Inicio
## Sorpresa
## Repaso
## Accediendo a kubernetes (kubeconfig, kubectl, dashboard, curl)

## Accediendo a kubernetes cli

## Instalando kubectl
> Instalando kubectl
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(<kubectl.sha256)  kubectl" | sha256sum --check
chmod +x kubectl
mv kubectl use_programs
```
## Iniciando el cluster de minikube
```bash
minikube start
```
## Ahora si Instalando kubectl
## Revisando las addons de minikube
```bash
minikube addons list
```
## Habilitando el addon de dashboard en minikube
```bash
minikube addons enable dashboard
```
## Habilitando el addon de metrics-server en minikube
```bash
minikube addons enable metrics-server
```
## Validando la instalacion de los addons
```bash
minikube addons list
```
## Accediendo al  dashboard
```bash
minikube dashboard
```
> Link de acceso al dashboard:
> http://localhost:37751/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

## Archivo de configuracion kubeconfig
> Metodo 1
```bash
cat $HOME/.kube/config
```
> Metodo 2
```bash
kubectl config view
```
## Creando nuestro request hacia el control-plane
> Identificar la IP del API-server de kubernetes
```bash
kubectl config view |grep -i server
```
> Obtener el token
```bash
kubectl describe secret -n kube-system default-xxxxx
EXPORT $TOKEN=secret.value
```

> Exportar el APISERVER
```bash
APISERVER=$(kubectl config view | grep https | cut -f 2- -d ":" | tr -d " ")
```

> Hacer el request hacia nuestro cluster de kubernetes
```bash
curl $APISERVER --header "Authorization: Bearer $TOKEN" --insecure
```
## Objetos en kubernetes
## Objetos de kubernetes - Modelo de objetos
## Que es un Pod
[cap04-01pod.yml](./devops-k8s-04/cap04-01pod.yml)
```bash
kubectl apply -f cap04-01pod.yml
```

## Que es un Label y un Selector
[cap04-02label.yml](./devops-k8s-04/cap04-02label.yml)
```bash
kubectl apply -f cap04-02label.yml
```
## Que es un Deployment
[cap04-03deployment.yml](./devops-k8s-04/cap04-03deployment.yml)
```bash
kubectl apply -f cap04-03deployment.yml
```
## Que es un NameSpace
[cap04-04namespace.yml](./devops-k8s-04/cap04-04namespace.yml)
```bash
kubectl apply -f cap04-04namespace.yml
```
## Resumen del capitulo