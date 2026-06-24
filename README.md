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

**Ressources déployées :** `ConfigMap`, `Secret`, `Deployment`, `Service` (ClusterIP + NodePort)

**Concepts démontrés :**
- Référencement de `ConfigMap` et `Secret` dans les variables d'environnement des pods
- Différence entre `ClusterIP` (interne) et `NodePort` / `LoadBalancer` (externe)
- Accès à l'UI via `minikube service`

### Projet 2 — Mosquitto MQTT Broker avec Volumes

**Ressources déployées :** `ConfigMap` (fichier de config), `Secret` (certificat SSL), `Deployment` + `Service`

**Concepts démontrés :**
- Montage de `ConfigMap` et `Secret` comme **fichiers** (pas seulement des variables d'env)
- `subPath` pour monter un fichier unique sans écraser le répertoire entier
- `volumes` et `volumeMounts` dans un Deployment

---

## EN — Description

This project covers Kubernetes fundamentals through two projects deployed on a local Minikube cluster.

### Project 1 — MongoDB + Mongo Express

**Deployed resources:** `ConfigMap`, `Secret`, `Deployment`, `Service` (ClusterIP + NodePort)

**Concepts demonstrated:**
- Referencing `ConfigMap` and `Secret` in pod environment variables
- Difference between `ClusterIP` (internal) and `NodePort` / `LoadBalancer` (external)
- Accessing the UI via `minikube service`

### Project 2 — Mosquitto MQTT Broker with Volumes

**Deployed resources:** `ConfigMap` (config file), `Secret` (SSL certificate), `Deployment` + `Service`

**Concepts demonstrated:**
- Mounting `ConfigMap` and `Secret` as **files** (not just env variables)
- `subPath` to mount a single file without overwriting the entire directory
- `volumes` and `volumeMounts` in a Deployment

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
