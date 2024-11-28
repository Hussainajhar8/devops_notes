# Kubernetes Notes

These notes cover important topics related to Kubernetes that I have identified while preparing for the Certified Kubernetes Administrator certification exam. I have included examples and explanations to help me better understand these concepts and fill any gaps in my knowledge. These notes will serve as a valuable resource for me to review and revise before the exam.

## Certified Kubernetes Administrator (CKA) Guide

### Cluster Architecture

1. **Master Nodes**

- Responsible for managing the cluster's state.
- Handle planning, scheduling, and monitoring of worker nodes.
- Serve as the brain of the Kubernetes cluster.

2. **Worker Nodes**

- Host and run containerized applications.
- Receive tasks from the master nodes via the API server.

3. **ETCD**

- A distributed key-value database that stores all cluster data, including configuration and state.
- Acts as the source of truth for the cluster.

4. **Kube-Scheduler**

- Assigns pods to nodes based on resource requirements, constraints, and policies.
- Ensures optimal distribution of workloads across the cluster.

5. **Node Controller**

- Manages the lifecycle of nodes.
- Detects node failures and creates replacements when needed.

6. **Replication Controller**

- Ensures the desired number of replicas (containers) for a pod are running.
- Automatically scales up or down as required.

7. **Controller Manager**

- A daemon that manages all Kubernetes controllers.
- Includes replication controllers, endpoint controllers, namespace controllers, and others.

8. **Kube-API Server**

- Acts as the central communication hub for the cluster.
- Exposes the Kubernetes API to users, controllers, and worker nodes.
- Handles orchestration tasks and manages communication between components.

9. **Container Runtime Engine**

- The underlying software that runs containers on each node.
- Docker is a commonly used container runtime.

10. **Kubelet**

- An agent that runs on every worker node.
- Listens to the Kube-API Server for instructions and manages containers on its node.

11. **Kube-Proxy**

- Runs on worker nodes to manage network rules.
- Ensures seamless communication between services and pods within the cluster.
