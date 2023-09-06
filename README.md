# K8S-react

Proyecto final Docker aplicación react con nodejs, postgres y nginx 

- _los siguientes comandos deben ejecutarse respectivamente en cada carpeta_
- _Para más informacion consultar documento de proyecto_

---
### Dentro de la carpeta server
---
Probar localmente aplicación server http://localhost:5000/
```sh
npm run dev
```
Para compilar archivo Dockerfile.dev http://localhost:4003/
```sh
docker build -f Dockerfile.dev -t carolinabermudez/multi-server .
docker run -it -p 4003:5000 carolinabermudez/multi-server
```

Para compilar archivo Dockerfile http://localhost:4002/
```sh
docker build -t carolinabermudez/multi-server .
docker run -it -p 4002:5000 carolinabermudez/multi-server
docker push carolinabermudez/multi-server
```
---
### Dentro de la carpeta cliente
---
Probar localmente aplicación client http://localhost:3000/
```sh
npm run start
```
Para compilar archivo Dockerfile.dev http://localhost:4002/
```sh
docker build -f Dockerfile.dev -t carolinabermudez/multi-client .
docker run -it -p 4002:3000 carolinabermudez/multi-client
```
Para compilar archivo Dockerfile
```sh
docker build -t carolinabermudez/multi-client .
docker run -it -p 3000:3000 carolinabermudez/multi-client
docker push carolinabermudez/multi-client
```
---
### Dentro de la carpeta K8S-react
---
Para levantar todo con compose http://localhost:3050/
```sh
docker-compose up --build
```
Para crear la contraseña de la base de datos
```sh
kubectl create secret generic pgpassword --from-literal PGPASSWORD=12345test
kubectl get secrets
```
Para instalar el controlador de ingress-nginx
```sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.1/deploy/static/provider/cloud/deploy.yaml
```
Para instalar el controlador de ingress con minikube
```sh
minikube addons enable ingress
```
Para mostrar si se crearon bien los pods
```sh
kubectl get pods -n ingress-nginx
```
Para aplicar los manifestos de kubernetes y mostrarlos los recursos
```sh
kubectl apply -f k8s
kubectl get pods
kubectl get pv
kubectl get services
kubectl get deploy
```
Para acceder a la aplicacion http://localhost
```sh
minikube tunnel
```
---
### Comandos de ayuda
---
Para errores o problemas con wsl correr cmd como administrador los siguientes comandos que nos muestra el estado, si se encuentra como "Stopped" habrá que cambiarlo
```sh
wsl -l -vez 
wsl -d ubuntu dmesg -w
minikube start --driver=docker
systemctl enable kubelet.service
```
Para mostrar contenedores e imagenes com formato
```sh
docker image list --format "table {{.ID}}\t{{.CreatedSince}}\t{{.Repository}}"
docker container ls --format "{{.ID}}\t{{.Image}}\t{{.Status}}"
docker container ls --format "{{.ID}}\t{{.Names}}\t{{.Status}}\t{{.Ports}}"
```
Detener y eliminar contenedor
```sh
docker stop <Container_ID>
docker rm <Container_ID>
```
Forzar eliminar contenedor 
```sh
docker rm -f < Container_ID>
```
Eliminar imagen
```sh
docker rmi -f <Image_name>
```
Eliminar deployment
```sh
kubectl delete deployment <deploymentname>
```