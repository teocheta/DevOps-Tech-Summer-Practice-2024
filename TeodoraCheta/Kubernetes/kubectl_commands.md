# Kubernetes CLI Commands

## Basic Commands

### Check Status
- `$ kubectl get nodes`: Get the status of the nodes
- `$ kubectl get pod / services / deployment`: Get the status of pods, services, or deployments

### Create Components
- `$ kubectl create ...`: Create components
- `$ kubectl create deployment nginx-depl --image=nginx`: Create a deployment named `nginx-depl` with the specified image

## Layers of Abstraction

- **Deployment** manages -> **ReplicaSet** manages -> **Pod** manages -> **Container**
- Everything below the container should be managed by Kubernetes

## Editing Configurations

- `$ kubectl edit deployment [name]`: Edit the auto-generated configuration file for the specified deployment

## Debugging Pods

- `$ kubectl logs [pod name]`: View logs of the specified pod
- `$ kubectl describe pod [pod name]`: Get detailed information about the specified pod
- `$ kubectl exec -it [pod name] --bin/bash`: Access the terminal of the application inside the container
  - `$ exit`: Exit the terminal

## Deleting and Applying Deployments

- `$ kubectl delete deployment [name]`: Delete the specified deployment
- `$ kubectl apply -f [file name]`: Execute the configuration file to create or update a deployment

---

These commands are essential for managing Kubernetes clusters, from creating and monitoring components to debugging and updating configurations.

