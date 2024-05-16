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
