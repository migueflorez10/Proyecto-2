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



## Referencias
- [Instalación de microk8s](https://microk8s.io/#install-microk8s)
- [Documentación de clustering en microk8s](https://microk8s.io/docs/clustering)
- [Cómo utilizar NFS en microk8s](https://microk8s.io/docs/how-to-nfs)
- [Video tutorial sobre microk8s](https://www.youtube.com/watch?v=3T6skoL3RTA&feature=youtu.be)
- [Imagen de Docker para MySQL en Bitnami](https://hub.docker.com/r/bitnami/mysql)
- [Imagen de Docker para WordPress](https://hub.docker.com/_/wordpress)
- [Tutorial de Kubernetes para aplicaciones stateful (MySQL y WordPress)](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/)




