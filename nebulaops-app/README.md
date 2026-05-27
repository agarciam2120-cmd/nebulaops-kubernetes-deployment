NebulaOps – Despliegue de aplicación Flask con Docker, KIND y Kubernetes

Este repositorio contiene todo lo necesario para desplegar una aplicación web desarrollada en Flask utilizando contenedores Docker y un clúster Kubernetes local creado con KIND (Kubernetes in Docker). El proyecto forma parte del Trabajo de Fin de Grado del CFGS Administración de Sistemas Informáticos en Red (ASIR).

El objetivo es demostrar un despliegue real con:

•	Contenerización mediante Docker

•	Orquestación con Kubernetes

•	Autoescalado mediante HPA

•	Métricas con metrics-server

•	Resiliencia ante fallos

•	Exposición del servicio mediante NodePort

Estructura del repositorio

Código

/app.py                 → Aplicación Flask

/requirements.txt       → Dependencias de Python

/Dockerfile             → Construcción de la imagen Docker



/deployment.yaml        → Deployment de Kubernetes

/service.yaml           → Service tipo NodePort

/hpa.yaml               → Horizontal Pod Autoscaler

/kind-config.yaml       → Configuración del clúster KIND

Requisitos previos

Para ejecutar el proyecto es necesario tener instalado:

•	Docker Desktop

•	WSL2 + Ubuntu (en Windows)

•	kubectl

•	kind

•	Cuenta en Docker Hub (para subir la imagen)

Cómo ejecutar el proyecto

1\. Clonar el repositorio

Código

git clone https://github.com/TU\_USUARIO/nebulaops-kubernetes-deployment.git

cd nebulaops-kubernetes-deployment

2\. Construir la imagen Docker

Código

docker build -t TU\_USUARIO/nebulaops:v1 .

3\. Iniciar sesión en Docker Hub

Código

docker login

4\. Subir la imagen al repositorio

Código

docker push TU\_USUARIO/nebulaops:v1

5\. Crear el clúster KIND

Código

kind create cluster --config kind-config.yaml

6\. Aplicar los manifiestos de Kubernetes

Código

kubectl apply -f deployment.yaml

kubectl apply -f service.yaml

kubectl apply -f hpa.yaml

7\. Verificar el despliegue

Código

kubectl get nodes

kubectl get pods

kubectl get deployment

kubectl get service

kubectl get hpa

8\. Acceder a la aplicación

Abrir el navegador y entrar en:

Código

http://localhost:30080

Autoescalado y métricas

Para generar carga y activar el HPA:

Código

while true; do curl http://localhost:30080 > /dev/null; done

Para observar el escalado en tiempo real:

Código

kubectl get pods -w

Resiliencia

Para comprobar la recreación automática de Pods:

Código

kubectl delete pod <nombre-del-pod>

kubectl get pods

Autor

Ángel García Martín CFGS Administración de Sistemas Informáticos en Red I.E.S. Venancio Blanco — Salamanca

Licencia

Este proyecto se distribuye bajo licencia Creative Commons BY-SA 3.0 ES.



