## 🏗️ Kubernetes Cluster Architecture Overview

This repository demonstrates a production-grade Kubernetes cluster setup, separated into a centralized management layer (Control Plane) and an isolated execution layer (Data Plane).
<img width="1163" height="912" alt="k8s-architecture png" src="https://github.com/user-attachments/assets/ff74b65a-1e05-4e0a-b528-cc6d001abd86" />

### 🧠 Control Plane (Master Node)
The administrative brain of the cluster, responsible for maintaining the desired state, scheduling workloads, and managing global configurations.

*   **`kube-apiserver`**: The front door to the cluster. Exposes the Kubernetes API and handles all internal and external REST communication.
*   **`etcd`**: A highly available, consistent key-value store used as the single source of truth for all cluster configuration data.
*   **`kube-scheduler`**: The placement engine. Monitors newly created Pods and assigns them to optimal worker nodes based on resource demands.
*   **`kube-controller-manager`**: The background regulation loop. Runs core controller processes (e.g., Node and Replication controllers) to maintain the cluster state.
*   **`cloud-controller-manager`**: Decouples cloud-specific infrastructure. Integrates the cluster natively with underlying cloud provider APIs for load balancers and storage.

### ⚙️ Data Plane (Worker Node 2)
The execution layer consisting of physical or virtual machines where containerized workloads are physically deployed and run.

*   **`kubelet`**: The primary node agent. Ensures that the assigned containers are healthy, running, and fully match the specifications defined in Pod specs.
*   **`kube-proxy`**: The network orchestrator. Runs on every node to manage routing rules, enabling network communication to Pods from inside or outside the cluster.
*   **`Container Runtime (containerd)`**: The underlying execution engine responsible for pulling images, isolating environments, and running the application containers.
*   **`Ingress Controller`**: The internal traffic router. Evaluates HTTP/HTTPS routing rules to direct external web traffic safely to target workloads.

### 🌐 Edge & Traffic Flow
*   **`Cloud Load Balancer`**: Sits outside the cluster border. Acts as the public entry point for incoming internet traffic, distributing requests across healthy nodes.
*   **`Pod C (Container 3)`**: The smallest deployable computing unit within the data plane, encapsulating the live application logic inside isolated containers.
