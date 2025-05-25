# Laboratorio K8s
Guia de instalación
## Actualizar Ubuntu Server
```
sudo apt update && sudo apt upgrade -y
```
## Instalación de Docker CE (Docker Engine Community Edition) 
```
sudo apt-get install -y ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg -- dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME}") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
sudo apt-get update
```
```
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Dar permisos a Docker para ejecutarse sin sudo

```
sudo usermod -aG docker $USER
newgrp docker
```

Verificar la instalación de Docker

```
docker run hello-world
```

## Instalar kubectl
```
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.33/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.33/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list > /dev/null
sudo apt-get update
```
Con el repositorio añadido, instalamos el paquete kubectl
```
sudo apt-get install -y kubectl
```
Verificar kubectl
```
kubectl version --client
```
## Instalar Minikube
Este comando descarga la última versión estable de Minikube
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
```
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
Configurar Minikube para usar Docker como driver predeterminado
```
minikube config set driver docker
```
Iniciar Minikube
```
minikube start --driver=docker
```
kubectl cluster-info muestra las direcciones del plano de control (API server) y servicios core del clúster.
```
kubectl cluster-info
```
kubectl get nodes listará los nodos del clúster
```
kubectl get nodes
```