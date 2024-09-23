## Introduction 

A DaemonSet in Kubernetes ensures that a copy of a specific pod runs on all or a selected group of nodes in a cluster. It’s typically used for system-level tasks or background services that need to be deployed universally across the nodes. Below are five examples of why you might need a DaemonSet, along with explanations:

1. Node Monitoring (e.g., Prometheus Node Exporter)
Use Case: Collecting metrics from each node.
Explanation: A DaemonSet can deploy a monitoring agent like Prometheus Node Exporter on every node to gather system metrics like CPU, memory, and disk usage for each node. This data is then used for monitoring and alerting.
2. Log Collection (e.g., Fluentd or Logstash)
Use Case: Centralized logging.
Explanation: A logging agent such as Fluentd can be deployed via a DaemonSet to ensure logs from all nodes are collected and sent to a centralized logging system (like Elasticsearch or Splunk) for analysis and storage.
3. Security and Compliance (e.g., Falco or Open Policy Agent)
Use Case: Security monitoring and enforcement.
Explanation: Tools like Falco, deployed through a DaemonSet, can monitor system calls on all nodes, alerting on abnormal behavior, potential intrusions, or policy violations to ensure security and compliance.
4. Storage Management (e.g., Ceph or GlusterFS)
Use Case: Managing distributed storage.
Explanation: In a distributed storage system, DaemonSets can be used to run storage agents on all nodes that participate in the storage cluster. This allows for uniform management of data replication, recovery, and availability across the nodes.
5. Network Management (e.g., Calico or Cilium)
Use Case: Configuring network policies and routing.
Explanation: Networking components like Calico or Cilium can be deployed using a DaemonSet to enforce networking policies, manage networking layers, and handle network traffic between pods and external systems, ensuring consistent networking across all nodes.
Summary
A DaemonSet is critical when you need a service or application to be running on every (or selected) node. It automates the process of ensuring that background processes or system-level components are deployed universally across your cluster.

DaemonSets can improve the performance of a Kubernetes cluster by distributing maintenance tasks and support services via deploying Pods across all nodes. They are well suited for long-running services like monitoring or log collectio

- From cli run this command and ensure all nodess are ready state

```
kubectl get nodes
```

## 1. Create a namespace daemonset
```
kubectl create ns daemonset
```
## 2 .Create a nginux demonset
```
kubectl apply -f https://raw.githubusercontent.com/careerbytecode/cloud-devops-engineer-training/main/5-kubernetes_admin/5-Daemonset/daemonset-nginx.yaml -n daemonset
```

```
kubectl get all -n daemonset
```

- see now daemonset is 2 and running in each worker/client node.because daemonset is mandatory for each worker or client node.

```
watch -n 1 kubectl get all -n daemonset -o wide
```

- after executed the above command,now go to gcp cloud kubernetes console and add one more worker node in the existing cluster

- now you should have 3 workernode in the GKE cluster


- go to cli and run the below command

```
kubectl get nodes
```
- you  must see all nodes are ready state.you see now 3 worker noder running in the above command

- see now daemonset is 3 and running in each worker/client node.because daemonset is mandatory for each worker or client node.

```
watch -n 1 kubectl get all -n daemonset -o wide
```
```
kubectl delete ns daemonset
```
