# Kubernetes: Open Source Container Orchestration Tool

## Why Kubernetes?

- Transition from monolith to microservices architecture

## Features

- **High Availability:** No downtime
- **Scalability:** High performance
- **Disaster Recovery:** Backup and restore

## Components

### 1. Node
- Simple server, physical or virtual machine

### 2. Pod
- Abstraction over a container
- Usually one application per pod
- Smallest unit of Kubernetes
- Each pod gets its own IP address
- Pods can die easily and get replaced, receiving a new IP address upon re-creation

### 3. Service
- Pods communicate with each other through services
- Provides a permanent IP address that can be attached to each pod
- Lifecycles of pods and services are not connected
- To make an app accessible through a browser, use an external service to open communication to external sources
- Use internal service for communication, e.g., with a database
- Load balancer directs traffic to the less busy pod

### 4. Ingress
- Manages URLs, secure protocols, and domain names

### 5. ConfigMap
- Stores external configuration of the app (e.g., database URL)
- Connected to the pod

### 6. Secret
- Stores secret data such as credentials (e.g., username, password)
- Data is base64 encoded

### 7. Volumes
- Persists data
- Attaches physical storage on a hard drive to a pod; can be local or remote (e.g., cloud storage)
- Not part of the Kubernetes cluster

### 8. Deployment
- Abstraction of pods
- Avoids downtime by replicating everything on other nodes, connected to the service
- Defines a blueprint to specify the number of replicas of a pod
- You create deployments, not individual pods, allowing you to scale up or down
- If one pod dies, the service forwards the request to another pod, keeping the app accessible to users
- Used for stateless applications

### 9. StatefulSet
- Cannot replicate a database using deployment due to its state (its data)
- Used for stateful applications
- Manages data inconsistencies

---

Kubernetes provides a robust platform for managing containerized applications, ensuring high availability, scalability, and efficient disaster recovery.

