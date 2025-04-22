# k8s-WorkLoads-StatefulSet
Maintains state and unique identity for pods

## `StatefulSet`
`Definition`: A StatefulSet manages the deployment and scaling of a set of pods, providing guarantees about the ordering and uniqueness of these pods, with stable network identities and persistent storage.

`Example`:
You're building a distributed database system for a financial application that requires data persistence and ordered operations.
You deploy MongoDB as a StatefulSet with 3 replicas. Each pod gets a predictable name (mongodb-0, mongodb-1, mongodb-2) and stable hostname that doesn't change even after pod restarts. 
The primary database runs on mongodb-0, with secondaries on the others. Each pod has its own persistent volume that stays associated with it. When a pod restarts, it reconnects to the same storage volume, maintaining data consistency. During scaling operations, pods are created and terminated in order, avoiding data corruption. Client applications connect to specific instances when they need to write to the primary.

## Kubernetes Workload Resources

Key differences between DaemonSet, StatefulSet, ReplicaSet, and Deployment in Kubernetes:

| Feature | DaemonSet | StatefulSet | ReplicaSet | Deployment |
|---------|-----------|-------------|------------|------------|
| **Purpose** | Runs a pod on every node in the cluster | Maintains state and unique identity for pods | Maintains a stable set of replica pods | High-level resource for deploying and updating applications |
| **Pod Identity** | Each pod is unique to a node | Each pod has persistent identity and stable hostname | Pods are interchangeable | Pods are interchangeable |
| **Scaling** | Automatically scales with nodes (one pod per node) | Manual or auto-scaling with ordered creation/deletion | Manual or auto-scaling with random creation/deletion | Manual or auto-scaling with random creation/deletion |
| **Pod Naming** | Usually `<name>-<node-name>` | `<name>-0`, `<name>-1`, etc. (ordered, sequential) | Random names with hash | Random names with hash |
| **Storage** | Typically uses node storage | Supports stable persistent storage per pod | Shared storage only | Shared storage only |
| **Load Balancing** | Not inherently load-balanced (one per node) | Not automatically load-balanced (identity matters) | Load-balanced (stateless) | Load-balanced (stateless) |
| **Updates** | Rolling updates possible | Ordered, sequential updates | All pods updated simultaneously | Rolling updates, canary deployments, rollbacks |
| **Use Cases** | Monitoring, logging, networking agents | Databases, messaging queues, stateful applications | Rarely used directly (deployment uses it) | Web applications, APIs, stateless workloads |
| **Deletion Order** | Random | Reverse order (highest to lowest index) | Random | Random |
| **Owns ReplicaSet** | No | No | No | Yes (manages ReplicaSets) |
