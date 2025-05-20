# Hacksheet de Minikube

Este es un resumen rápido de los comandos más comunes de Minikube.

**Iniciar y Detener**

* `minikube start`: Inicia el clúster de Minikube.
* `minikube stop`: Detiene el clúster de Minikube.
* `minikube delete`: Elimina el clúster de Minikube.

**Estado del Clúster**

* `minikube status`: Muestra el estado del clúster de Minikube.
* `kubectl cluster-info`: Muestra información sobre el clúster de Kubernetes gestionado por Minikube.

**Interactuar con el Clúster (usando kubectl)**

* `kubectl get nodes`: Lista los nodos del clúster.
* `kubectl get pods`: Lista los pods en el namespace por defecto.
* `kubectl get deployments`: Lista los deployments en el namespace por defecto.
* `kubectl create deployment <nombre> --image=<imagen>`: Crea un nuevo deployment.
* `kubectl expose deployment <nombre> --type=LoadBalancer --port=<puerto_interno> --target-port=<puerto_contenedor>`: Expone un deployment como un servicio.
* `kubectl logs <nombre_pod>`: Muestra los logs de un pod específico.
* `kubectl apply -f <archivo.yaml>`: Aplica una configuración desde un archivo YAML.

**Acceder al Clúster**

* `minikube service <nombre_servicio> --url`: Obtiene la URL para acceder a un servicio expuesto.
* `minikube dashboard`: Abre el dashboard de Kubernetes en el navegador.

**Configuración de Minikube**

* `minikube config view`: Muestra la configuración actual de Minikube.
* `minikube config set <propiedad> <valor>`: Establece una propiedad de configuración (ej: `minikube config set memory 4096`).

**Addons**

* `minikube addons list`: Lista los addons disponibles.
* `minikube addons enable <addon_nombre>`: Habilita un addon.
* `minikube addons disable <addon_nombre>`: Deshabilita un addon.

**Trucos Útiles**

* `minikube ssh`: Accede al nodo de Minikube mediante SSH.
* `minikube tunnel`: Crea un túnel de red para acceder a servicios con tipo LoadBalancer sin necesidad de un proveedor de nube.