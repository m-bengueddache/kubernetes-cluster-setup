# Kubernetes Cluster Setup

> **FR** — Mise en place d'un cluster Kubernetes local avec Minikube, déploiement de MongoDB avec ConfigMap/Secret, et déploiement d'un broker MQTT Mosquitto avec volumes et fichiers de configuration montés.
>
> **EN** — Local Kubernetes cluster setup with Minikube, MongoDB deployment with ConfigMap/Secret, and Mosquitto MQTT broker deployment with mounted volumes and configuration files.

---

## Stack

![Kubernetes](https://img.shields.io/badge/Kubernetes-Minikube-326CE5?logo=kubernetes)
![MongoDB](https://img.shields.io/badge/MongoDB-latest-green?logo=mongodb)
![Mosquitto](https://img.shields.io/badge/Eclipse%20Mosquitto-MQTT-3C5280)

---

## FR — Description

Ce projet couvre les fondamentaux de Kubernetes à travers deux projets déployés sur un cluster Minikube local.

### Projet 1 — MongoDB + Mongo Express

`ConfigMap`, `Secret`, `Deployment`, `Service` ClusterIP et NodePort.

Les variables d'environnement des pods référencent des valeurs depuis un `ConfigMap` (URL de connexion) et un `Secret` (credentials). Un service `ClusterIP` expose MongoDB en interne ; un `NodePort` expose Mongo Express depuis l'hôte via `minikube service`.

### Projet 2 — Mosquitto MQTT Broker avec Volumes

`ConfigMap` (fichier de config), `Secret` (certificat SSL), `Deployment` + `Service`.

Contrairement au projet 1, les `ConfigMap` et `Secret` sont montés comme des **fichiers** dans le conteneur, pas comme des variables d'environnement. `subPath` permet de monter un fichier unique sans écraser le répertoire de destination entier. `volumes` et `volumeMounts` wired dans le Deployment.

---

## EN — Description

This project covers Kubernetes fundamentals through two projects deployed on a local Minikube cluster.

### Project 1 — MongoDB + Mongo Express

`ConfigMap`, `Secret`, `Deployment`, `Service` (ClusterIP + NodePort).

Pod environment variables reference values from a `ConfigMap` (connection URL) and a `Secret` (credentials). A `ClusterIP` Service exposes MongoDB internally; a `NodePort` exposes Mongo Express from the host via `minikube service`.

### Project 2 — Mosquitto MQTT Broker with Volumes

`ConfigMap` (config file), `Secret` (SSL cert), `Deployment` + `Service`.

Unlike project 1, the `ConfigMap` and `Secret` are mounted as **files** in the container, not env variables. `subPath` mounts a single file without overwriting the entire destination directory. `volumes` and `volumeMounts` wired in the Deployment.

---

## Project Structure

```
.
├── mongodb/
│   ├── mongo-secret.yaml           # MongoDB credentials (base64)
│   ├── mongo-configmap.yaml        # MongoDB connection URL
│   ├── mongo.yaml                  # MongoDB Deployment + ClusterIP Service
│   └── mongo-express.yaml          # Mongo Express Deployment + NodePort Service
└── mosquitto/
    ├── config-file.yaml            # ConfigMap: mosquitto.conf
    ├── secret-file.yaml            # Secret: SSL certificate
    ├── mosquitto.yaml              # Deployment + Service with volume mounts
    └── mosquitto-without-volumes.yaml
```
