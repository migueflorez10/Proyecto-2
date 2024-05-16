# Link de Sustentación:
[Ver Sustentación Reto 4](https://eafit-my.sharepoint.com/:v:/g/personal/mamartinef_eafit_edu_co/Ef8i9vlrlONAnRIpJaXIIb8BIJnZ1HGRPCTxaS8LNOoW3A?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D&e=tFMvv2)


### Info de la Materia: Topicos Especiales en Telematica-st0263

### Estudiantes:
- Miguel Angel Martinez Florez, mamartinef@eafit.edu.co
- Mateo Muñoz Cadavid, mmunozc4@eafit.edu.co

### Profesor:  Edwin Nelson Montoya Munera, emontoya@eafit.edu.co  

# Proyecto 2: Cluster Kubernetes

##  Objetivo
El objetivo principal de este proyecto es desplegar la misma aplicación del Reto 4 en un clúster de alta disponibilidad en Kubernetes utilizando microk8s como IaaS en la nube de
Google Cloud Platform (GCP). Se busca configurar un clúster de Kubernetes propio, montar un servidor NFS para manejar volúmenes compartidos, y garantizar alta disponibilidad en 
todas las capas de la aplicación, incluyendo la capa de aplicación, base de datos y almacenamiento.

## Descripción de la Actividad
En este proyecto, se implementará un clúster de Kubernetes en GCP utilizando microk8s en al menos tres máquinas virtuales. Se desplegará la misma aplicación monolítica de WordPress 
utilizada en el Reto 4, pero esta vez en un entorno de alta disponibilidad configurado manualmente, en lugar de utilizar un clúster gestionado como AWS EKS. Se implementarán 
balanceadores de carga, alta disponibilidad en todas las capas de la aplicación, y se permitirá el aumento dinámico de nodos en el clúster Kubernetes.

## Arquitectura del Reto
![image](https://github.com/migueflorez10/Proyecto-2/assets/68928440/d0a6ce8e-65fe-4162-8064-a2e70f1e1195)

La arquitectura del proyecto consiste en un clúster de Kubernetes en GCP con al menos tres nodos, cada uno ejecutando microk8s. Se utilizará un servidor NFS desplegado en el 
clúster para manejar volúmenes compartidos. Se implementará un balanceador de carga para la capa de aplicación, y se desplegará una base de datos de alta disponibilidad 
en Kubernetes. El sistema se accederá a través de un nombre de dominio configurado para el servicio.

La arquitectura consta de los siguientes componentes principales:
- **Google Cloud Platform (GCP):** La infraestructura de la nube utilizada para desplegar el clúster de Kubernetes y los servicios relacionados. Se emplea GCP por su escalabilidad, confiabilidad y facilidad de uso.
- **Clúster de Kubernetes:** Se instala un clúster de Kubernetes con microk8s en al menos tres máquinas virtuales en GCP. Este clúster será la base sobre la cual se desplegará la aplicación de WordPress y se configurarán los servicios necesarios para garantizar alta disponibilidad.
- **Servidor NFS:** Se monta un servidor NFS (Network File System) en el clúster de Kubernetes para manejar volúmenes compartidos entre los nodos. Esto permite que los diferentes pods accedan a los mismos datos de manera consistente.
- **Balanceador de Carga:** Se implementa un balanceador de carga para distribuir el tráfico de red de manera equitativa entre los diferentes pods de la aplicación. Esto garantiza que la carga se distribuya de manera eficiente y se eviten cuellos de botella.
- **Alta Disponibilidad en Capa de Aplicación:** Se configura la aplicación de WordPress para garantizar su alta disponibilidad. Esto implica tener múltiples réplicas de los pods que ejecutan la aplicación y utilizar mecanismos de tolerancia a fallos para garantizar su disponibilidad en caso de errores.
- **Alta Disponibilidad en Capa de Base de Datos:** Se despliega una base de datos de alta disponibilidad en Kubernetes para respaldar la aplicación de WordPress. Esto se logra mediante la configuración de réplicas de la base de datos y la implementación de mecanismos de recuperación ante fallos.
- **Alta Disponibilidad en Capa de Almacenamiento:** Se utiliza el servidor NFS montado en el clúster de Kubernetes para garantizar la disponibilidad de los datos de la aplicación. El servidor NFS proporciona un almacenamiento persistente que es accesible por todos los pods de la aplicación.
- **Dominio Personalizado:** Se configura un nombre de dominio personalizado (por ejemplo, https://proyecto2.dominio.tld) para acceder al servicio desplegado en el clúster de Kubernetes. Esto permite que la aplicación sea accesible de forma pública a través de Internet.

## Descripción del Ambiente de Desarrollo y Técnico
El ambiente de desarrollo para este proyecto se basa en Google Cloud Platform (GCP), utilizando microk8s para la instalación del clúster de Kubernetes. Se utilizará GitHub para el control de versiones del código y la documentación del proyecto. Se requerirá un profundo conocimiento de Kubernetes, microk8s, y la configuración de servicios de alta disponibilidad en la nube.


## Guia paso a paso
1) Creación de las instancias(mircrok8s-master, microk8s-worker1, microk8s-worker2, microk8s-nfs):
- Se modifican los discos de arranque de las máquinas virtuales y se configura el firewall.
![image](https://github.com/migueflorez10/Proyecto-2/assets/68928440/30fea12d-688b-4899-ada2-d79779dc1383)
![image](https://github.com/migueflorez10/Proyecto-2/assets/68928440/5d607cbc-5c9e-46fb-833e-4919a64dbb91)

2)  Actualización de la máquina virtual:
- Se ejecuta el siguiente comando para actualizar la máquina virtual:
```
sudo apt-get update
```

3) Instalación de Microk8s en Ubuntu:
- Se instala Microk8s en Ubuntu utilizando el siguiente comando:
```
sudo snap install microk8s --classic
```

4) Verificación del estado de Kubernetes:
- Se verifica el estado de Kubernetes utilizando el siguiente comando:
```
microk8s status --wait-ready
```

5) Configuración de permisos:
- Si se muestra un mensaje de falta de permisos, se crea el directorio ./kube y se copian los comandos proporcionados. Luego, se reinicia la máquina para aplicar
los permisos necesarios.

6) Inicio de servicios necesarios:
- Se habilitan los servicios necesarios con el siguiente comando:
```
microk8s enable dashboard dns registry istio ingress
```

7) Creación del cluster
- En la instancia maestro, se ejecuta el siguiente comando para obtener el comando necesario para unir un nodo al clúster:
```
microk8s add-node
```
- debe aparecer un mensaje así.
![image](https://github.com/migueflorez10/Proyecto-2/assets/68928440/5eb29405-a44c-400e-af85-5d6b320443b8)
![image](https://github.com/migueflorez10/Proyecto-2/assets/68928440/7dda415d-7070-462a-ba3d-ccdacbacb989)


- Se debe copiar el comando de "join" que aparece como resultado de este comando.
![image](https://github.com/migueflorez10/Proyecto-2/assets/68928440/2460e949-30fb-4456-9ef7-c142dbc00475)

- Verificación de nodos en el maestro:
Para verificar que todos los nodos están correctamente unidos al clúster, se ejecuta el siguiente comando en el maestro:
```
microk8s kubectl get nodes
```

- Debería aparecer algo así:
![image](https://github.com/migueflorez10/Proyecto-2/assets/68928440/79b89cbf-db16-4bc6-9ef1-1a8f6120896a)

8) Configuración del NFS-Server:
- Se crea una máquina Ubuntu 22.04 con un disco de arranque de 20GB y se habilita el tráfico HTTP, HTTPS y las verificaciones de balanceador de cargas.
- Una vez creada, se actualiza la máquina y se instala el servidor de NFS:
```
sudo apt-get update
sudo apt-get install nfs-kernel-server
```

- Se procede a crear el directorio que se compartirá a los clientes NFS y se le otorgan los permisos necesarios:
```
sudo mkdir -p /srv/nfs
sudo chown nobody:nogroup /srv/nfs
sudo chmod 0777 /srv/nfs
```

- Luego, se edita el archivo `exports` para permitir el vínculo de este directorio:
```
sudo mv /etc/exports /etc/exports.bak
echo '/srv/nfs *(rw,sync,no_subtree_check)' | sudo tee /etc/exports
```

- Finalmente, se reinicia el servicio y se verifica que esté funcionando correctamente:
```
sudo systemctl restart nfs-kernel-server
sudo systemctl status nfs-kernel-server
```

- Instalación de los drivers CSI para NFS:
  - Desde la máquina MASTER, se habilita el paquete de Helm 3 y se obtienen los drivers:
  sudo systemctl status nfs-kernel-server
  ```
  microk8s enable helm3
  microk8s helm3 repo add csi-driver-nfs https://raw.githubusercontent.com/kubernetes-csi/csi-driver-nfs/master/charts
  microk8s helm3 repo update
  sudo systemctl status nfs-kernel-server
  ```
- Se descarga el helm chart del namespace de kube-system:
   ```
  microk8s helm3 install csi-driver-nfs csi-driver-nfs/csi-driver-nfs \
    --namespace kube-system \
    --set kubeletDir=/var/snap/microk8s/common/var/lib/kubelet
   ```

- Se espera hasta que estén los pods, lo cual se verifica con el siguiente comando:
   ```
   microk8s kubectl wait pod --selector app.kubernetes.io/name=csi-driver-nfs --for condition=ready --namespace kube-system
   ```

- Una vez que los pods estén listos, se verifica que los drivers CSI estén disponibles:
  ```
  microk8s kubectl get csidrivers
  ```

- Y debe verse un output similar al siguiente:
  ```
  NAME             ATTACHREQUIRED   PODINFOONMOUNT   STORAGECAPACITY   TOKENREQUESTS   REQUIRESREPUBLISH   MODES        AGE
  nfs.csi.k8s.io   false            false            false             <unset>         false               Persistent   39m
  ```

9) Posteriormente, se crean los archivos sc-nfs.yaml y pvc-nfs.yaml con el siguiente contenido:
- sc-nfs.yaml:
```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: nfs-csi
provisioner: nfs.csi.k8s.io
parameters:
  server: 0.0.0.0 #ip del nfs-server
  share: /srv/nfs
reclaimPolicy: Delete
volumeBindingMode: Immediate
mountOptions:
  - hard
  - nfsvers=4.1
```

- pvc-nfs.yaml:
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  storageClassName: nfs-csi
  accessModes: [ReadWriteOnce]
  resources:
    requests:
      storage: 5Gi
```

- Estos archivos se aplican con los siguientes comandos:
```
microk8s kubectl apply -f sc-nfs.yaml
microk8s kubectl apply -f pvc-nfs.yaml
```
Una vez se ejecuten estos comandos, el Persistent Volume Claim (PVC) debería haberse vinculado correctamente. Además, se podrá ver en el servidor NFS el PVC en el directorio compartido especificado.

10) Configuración de manifiestos MySQL, Wordpress e Ingress:
En esta sección vamos a crear los manifiestos para los diferentes servicios que se utilizarán en el proyecto, todos los cuales se encuentran en la carpeta Scripts con los datos específicos para este proyecto.

- MySQL: Primero, creamos el archivo `mysql-pv-pvc.yaml`:
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv
spec:
  storageClassName: nfs-csi
  capacity:
    storage: 5Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  nfs:
    server: 0.0.0.0 #ip del nfs-server
    path: /srv/nfs #cambiar por la ruta escogida
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pvc
  labels:
    app: mysql
spec:
  storageClassName: nfs-csi
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 5Gi
```

Se debe remplazar <contraseña>, <base_de_datos>, <usuario> por los datos reales.

- Aplicamos el manifiesto para comprobar que funcione correctamente:
```
microk8s kubectl apply -f mysql-pv-pvc.yaml
```

- Para verificar que se haya vinculado correctamente el PVC, utilizamos:
```
microk8s kubectl get pvc
```

- Wordpress: Creamos el archivo `wordpress-pv-pvc.yaml`:
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: wordpress-pv
spec:
  capacity:
    storage: 5Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  storageClassName: nfs-csi
  nfs:
    server: 0.0.0.0 #ip del nfs-server
    path: /srv/nfs #cambiar por la ruta escogida
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: wordpress-pvc
  labels:
    app: wordpress
spec:
  accessModes:
    - ReadWriteMany
  storageClassName: nfs-csi
  resources:
    requests:
      storage: 5Gi
```

Se debe remplazar <host_base_de_datos>, <contraseña>, <usuario>, <base_de_datos> por los datos reales.

- Aplicamos los manifiestos y verificamos que los PVC y los pods se hayan creado correctamente:
```
microk8s kubectl apply -f wordpress-pv-pvc.yaml
microk8s kubectl get pvc
microk8s kubectl apply -f wordpress-deployment.yaml
microk8s kubectl get pods
```

- Ingress: Creamos el archivo `ing-wordpress.yaml`:
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: http-ingress
  labels:
    app: wordpress
spec:
  rules:
  - http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          service:
            name: wordpress
            port:
              number: 80
```

- Aplicamos el manifiesto:
```
microk8s kubectl apply -f ing-wordpress.yaml
```

Una vez completada la configuración anterior, podemos acceder a la página de configuración de Wordpress utilizando la IP pública de la máquina MASTER en un navegador web. Al ingresar, se mostrará la página de configuración inicial de Wordpress, donde podemos llenar los datos requeridos, como nombre de la página, usuario y contraseña de administrador, y detalles de la base de datos.

Al completar esta configuración inicial, tendremos nuestra página de Wordpress funcionando correctamente en el clúster Kubernetes configurado. Podemos comenzar a agregar contenido y personalizar la página según nuestras necesidades.

![image](https://github.com/migueflorez10/Proyecto-2/assets/68928440/68217168-7022-4af7-868f-e320530a82ed)
![image](https://github.com/migueflorez10/Proyecto-2/assets/68928440/43c80166-e5b1-49ef-8bf0-6fe0940c9f6b)

11) Configuración de Certificación SSL:
- Antes de comenzar con este paso, debes agregar el registro para la IP pública de la máquina MASTER en tu servidor DNS.
  - nstalación de cert-manager:
    Instala cert-manager ejecutando el siguiente comando:
    ```
    microk8s kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.3.1/cert-manager.yaml
    ```

    Verifica que cert-manager se haya instalado correctamente con el siguiente comando:
     ```
     microk8s kubectl get pods -n=cert-manager
     ```
  - Creación de claves .pem:
    Genera las claves .pem para los archivos cluster-issuer-staging.yaml y cluster-issuer.yaml con los siguientes comandos:
    ```
    openssl genrsa -out letsencrypt-staging.pem 2048
    openssl genrsa -out letsencrypt-private-key.pem 2048
    ```

    Luego, crea un secreto en Kubernetes con estas claves:
    ```
    sudo microk8s kubectl create secret generic letsencrypt-staging --from-file=letsencrypt-staging.pem
    sudo microk8s kubectl create secret generic letsencrypt-private-key --from-file=letsencrypt-private-key.pem
    ```

  - Creación de ClusterIssuer:
    Crea los manifiestos cluster-issuer-staging.yaml y cluster-issuer.yaml con los siguientes contenidos:
     ```
     # cluster-issuer-staging.yaml
    apiVersion: cert-manager.io/v1
    kind: ClusterIssuer
    metadata:
      name: letsencrypt-staging
    spec:
      acme:
        email: tucorreo@gmail.com
        server: https://acme-staging-v02.api.letsencrypt.org/directory
        privateKeySecretRef:
          name: letsencrypt-staging
        solvers:
          - http01:
              ingress:
                class: public
     ```

     ```
     # cluster-issuer.yaml
    apiVersion: cert-manager.io/v1
    kind: ClusterIssuer
    metadata:
      name: letsencrypt-prod
    spec:
      acme:
        email: tucorreo@gmail.com
        server: https://acme-v02.api.letsencrypt.org/directory
        privateKeySecretRef:
          name: letsencrypt-private-key
        solvers:
          - http01:
              ingress:
                class: public
     ```

  - Aplica los manifiestos:
      ```
      microk8s kubectl apply -f cluster-issuer-staging.yaml
      microk8s kubectl apply -f cluster-issuer.yaml
      ```

  

  







## Referencias
- [Instalación de microk8s](https://microk8s.io/#install-microk8s)
- [Documentación de clustering en microk8s](https://microk8s.io/docs/clustering)
- [Cómo utilizar NFS en microk8s](https://microk8s.io/docs/how-to-nfs)
- [Video tutorial sobre microk8s](https://www.youtube.com/watch?v=3T6skoL3RTA&feature=youtu.be)
- [Imagen de Docker para MySQL en Bitnami](https://hub.docker.com/r/bitnami/mysql)
- [Imagen de Docker para WordPress](https://hub.docker.com/_/wordpress)
- [Tutorial de Kubernetes para aplicaciones stateful (MySQL y WordPress)](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/)




