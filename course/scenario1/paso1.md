# Paso 1 : Conociendo Pods
En este paso, aprenderás a crear un pod en Kubernetes, aprenderás a usar kubectl y a crear un pod de nginx.

## 1.1. Crear un Pod
Para crear un pod en Kubernetes, utilizaremos el comando `kubectl run`. Este comando nos permite crear un pod a partir de una imagen de contenedor. En este caso, utilizaremos la imagen de nginx.

```bash
kubectl run nginx --image=nginx
```

## 1.2. Verificar el estado del Pod
Para verificar el estado del pod, utilizaremos el comando `kubectl get pods`. Este comando nos mostrará una lista de todos los pods en el clúster y su estado.

```bash
kubectl get pods
```
## 1.3. Acceder al Pod  
Para acceder al pod, utilizaremos el comando `kubectl exec`. Este comando nos permite ejecutar un comando dentro de un contenedor en un pod. En este caso, utilizaremos el comando `bash` para acceder a la línea de comandos del contenedor.

```bash
kubectl exec -it nginx -- /bin/bash
```
## 1.4. Verificar la IP del Pod
Para verificar la IP del pod, utilizaremos el comando `kubectl get pods -o wide`. Este comando nos mostrará una lista de todos los pods en el clúster, su estado y su dirección IP.

```bash
kubectl get pods -o wide
```
## 1.5. Verificar los logs del Pod
Para verificar los logs del pod, utilizaremos el comando `kubectl logs`. Este comando nos permite ver los logs de un contenedor en un pod. En este caso, utilizaremos el nombre del pod que creamos anteriormente.

```bash
kubectl logs nginx
```
## 1.6. Eliminar el Pod
Para eliminar el pod, utilizaremos el comando `kubectl delete pod`. Este comando nos permite eliminar un pod del clúster. En este caso, utilizaremos el nombre del pod que creamos anteriormente.

```bash
kubectl delete pod nginx
```
## 1.7. Verificar que el Pod fue eliminado
Para verificar que el pod fue eliminado, utilizaremos el comando `kubectl get pods`. Este comando nos mostrará una lista de todos los pods en el clúster y su estado.

```bash
kubectl get pods
```
## 1.8. Crear un Pod con un archivo de configuración
Para crear un pod con un archivo de configuración, utilizaremos el comando `kubectl apply`. Este comando nos permite aplicar un archivo de configuración en formato YAML. En este caso, utilizaremos un archivo de configuración llamado `pod.yaml`.

el contenido del archivo `pod.yaml` es el siguiente:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
    containers:
    - name: nginx
        image: nginx
        ports:
        - containerPort: 80
```


## 1.9. Aplicar el archivo de configuración
Para aplicar el archivo de configuración, utilizaremos el comando `kubectl apply`. Este comando nos permite aplicar un archivo de configuración en formato YAML. En este caso, utilizaremos el archivo de configuración que creamos anteriormente.


```bash
kubectl apply -f pod.yaml
```

## 1.10 Verificar el estado del Pod
Para verificar el estado del pod, utilizaremos el comando `kubectl get pods`. Este comando nos mostrará una lista de todos los pods en el clúster y su estado.

```bash
kubectl get pods
```
## 1.11. Liveness y Readiness Probes 
Ahora que tenemos un pod en ejecución, vamos a aprender sobre las sondas de liveness y readiness. Estas sondas nos permiten verificar el estado de un contenedor y asegurarnos de que está listo para recibir tráfico.
## 1.12. Liveness Probe
La sonda de liveness nos permite verificar si un contenedor está en funcionamiento. Si la sonda falla, Kubernetes reiniciará el contenedor. Para agregar una sonda de liveness a nuestro pod, utilizaremos el siguiente archivo de configuración:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
    livenessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 5
```
## 1.13. Readiness Probe
La sonda de readiness nos permite verificar si un contenedor está listo para recibir tráfico. Si la sonda falla, Kubernetes no enviará tráfico al contenedor. Para agregar una sonda de readiness a nuestro pod, utilizaremos el siguiente archivo de configuración:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
    readinessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 5
```
## 1.14 Other Probes 
Además de las sondas de liveness y readiness, Kubernetes también admite sondas de tipo TCP y Exec. Estas sondas se utilizan para verificar el estado de un contenedor de diferentes maneras.
## 1.15. TCP Probe
La sonda TCP nos permite verificar si un contenedor está escuchando en un puerto específico. Si la sonda falla, Kubernetes reiniciará el contenedor. Para agregar una sonda TCP a nuestro pod, utilizaremos el siguiente archivo de configuración:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
    livenessProbe:
      tcpSocket:
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 5
```
