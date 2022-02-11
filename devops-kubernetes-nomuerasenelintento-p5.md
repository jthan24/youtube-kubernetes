# devops-kubernetes-nomuerasenelinteto-p5
https://youtu.be/djtbxtQaWes


## Inicio
## Repositorio de github (https://github.com/jthan24/youtube-kubernetes)
## Iniciando la presentacion
## Autenticacion, autorizacion y control de adminision
## Comunicacion hacia el cluster
## Autenticacion
## Accediendo al cluster con Token

```bash
TOKEN=$(kubectl describe secret -n kube-system $(kubectl get secrets -n kube-system | grep default | cut -f1 -d ' ') | grep -E '^token' | cut -f2 -d':' | tr -d '\t' | tr -d " ")
APISERVER=$(kubectl config view | grep https | cut -f 2- -d ":" | tr -d " ")
curl $APISERVER --header "Authorization: Bearer $TOKEN" --insecure
```

## Accediendo al clustter con Certificados

```bash
ENCODED_CERT=$(kubectl config view |grep client-certificate |cut -d: -f2 |tr -d " ")
ENCODED_KEY=$(kubectl config view |grep client-key|cut -d: -f2 |tr -d " ")
ENCODED_CA=$(kubectl config view |grep certificate-authority|cut -d: -f2 |tr -d " ")
curl $APISERVER --cert $ENCODED_CERT --key $ENCODED_KEY --cacert $ENCODED_CA
```

## Autorizacion
## Autorizacion role rolebinding kubectl 

```bash
kubectl create role pod-reader --verb=get --verb=list --verb=watch --resource=pods
kubectl create rolebinding bob-reader-binding --role=pod-reader --user=bob --namespace=default
```

## Admission control 
## Ejemplo de autenticacion y de autorizacion
### Creacion del usuario 
[01-signing-request.yaml](./devops-k8s-05/rbac/01-signin-request.yaml)

```bash
openssl genrsa -out bob.key 2048
openssl req -new -key bob.key -out bob.csr -subj "/CN=bob/O=learner"
vim 01-signing-request.yaml
cat bob.csr | base64 | tr -d '\n','%'
kubectl create -f 01-signing-request.yaml
kubectl get csr

kubectl certificate approve bob-csr
kubectl get csr
kubectl get csr bob-csr -o yaml
```

### Creacion de namespace
```bash
kubectl create namespace elejemplo
```

### Actualizando el kubeconfig

```bash
kubectl config set-credentials bob --client-certificate=bob.crt --client-key=bob.key
kubectl config set-context bob-context --cluster=minikube --namespace=elejemplo --user=bob

kubectl config view

kubectl -n elejemplo create deployment nginx --image=nginx:alpine

kubectl --context=bob-context get pods  #esto va a fallar, por que no hemos hecho el role ni el binding
```


### Creacion del role 
[02-role.yaml](./devops-k8s-05/rbac/02-role.yaml)
```bash
kubectl create -f 02-role.yaml
kubectl -n elejemplo get roles
```

### Creacion del rolebinding
[03-rolebinding.yaml](./devops-k8s-05/rbac/03-rolebinding.yaml)
```bash
kubectl create -f 03-rolebinding.yaml
kubectl -n elejemplo get rolebindings
kubectl --context=bob-context get pods
```


## Lo que falla en el "en vivo"
## Resumen del capitulo
