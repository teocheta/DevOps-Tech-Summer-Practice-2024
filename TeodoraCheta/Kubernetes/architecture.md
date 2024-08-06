# Node Processes

## Worker Nodes
- **Each Node:** Hosts multiple pods
- **Essential Processes on Every Worker Node:**
  - **Container Runtime:** (e.g., Docker)
  - **Kubelet:** Interacts with the container and node, starts the pod with a container inside, assigns resources
  - **Kube Proxy:** Forwards requests from services to pods with low overhead

## Master Nodes

### How to Interact with the Cluster
- **Master Nodes**: Manage the cluster

## Master Processes

### Essential Processes on Every Master Node
1. **API Server**
   - Cluster gateway
   - Initial request handler for any updates in the cluster, queries
   - Handles authentication
   - Validates requests and forwards them to other processes
   - The single entry point into the cluster

2. **Scheduler**
   - Decides on which worker node to schedule the pod
   - Kubelet executes the request on the chosen node
   - Analyzes resource needs and availability of worker nodes

3. **Controller Manager**
   - Detects state changes of pods (e.g., when pods die)
   - Requests the scheduler to reschedule those pods

4. **etcd**
   - Key-value store of the cluster state
   - Acts as the cluster's brain
   - Stores cluster changes, not the actual application data

## Example Cluster Setup

- **Typical Configuration:**
  - 2 master nodes
  - 3 worker nodes (small cluster)
  
- **Resource Allocation:**
  - Master nodes typically require fewer resources (CPU, RAM, Storage)
  
- **Adding Nodes:**
  - Acquire a new bare server
  - Install all necessary processes
  - Add it to the cluster

---

This setup ensures efficient management and operation of a Kubernetes cluster, with master and worker nodes fulfilling distinct but complementary roles.


