## Introduction 

A Pod can have multiple containers running apps within it, but it can also have one or more init containers, which are run before the app containers are started.

Init containers are exactly like regular containers, except:

Init containers always run to completion.
Each init container must complete successfully before the next one starts.


Init containers in Kubernetes serve a crucial role in preparing the environment for the main application containers. They are executed before the main container starts, and they can help manage dependencies, setup tasks, or initialize configurations. Here are five examples of why init containers are useful:

1. **Dependency Setup**
Example: Imagine you have a web application that relies on a database. You can use an init container to check if the database is up and running before starting the main application.
Explanation: The init container can ensure that the required dependencies (like a database service) are available. It prevents the main container from failing due to missing dependencies.

2. **File/Configuration Initialization**
Example: You might need to download configuration files from an external source (like a cloud storage bucket or a remote repository) before starting the main application.
Explanation: An init container can be used to pull these configuration files, perform transformations if needed, and place them in a shared volume so that the main container can use them at startup.

3. **Security Checks**
Example: A security-focused init container could run vulnerability scans or security checks (like scanning for vulnerabilities in dependencies) before allowing the main container to launch.
Explanation: This ensures that the main application only starts after passing certain security validations, improving the security posture of your workload.

4. **Waiting for Services to Be Ready**
Example: If the main application depends on several microservices, an init container can poll for their readiness (such as checking the readiness of an API or service).
Explanation: Instead of the main container failing and restarting, the init container waits until all the necessary services are available, avoiding unnecessary restarts.

5. **Data Migration or Setup**
Example: In cases where your application needs to perform a database schema migration before launching, the init container can handle this task.
Explanation: Running a schema migration or data transformation in an init container ensures that the database is in the correct state before the main application starts, preventing issues related to incompatible schema versions.
These examples highlight how init containers add flexibility, reliability, and robustness to your Kubernetes deployments by preparing the environment in a way that the main container can depend on.

```
kubectl get nodes
```

- the above command output should show all nodes are ready state.


## 1 . Create a namespace app1

- create new namespace called app1

```
kubectl create ns app1
```
## 2 . Create a node server
```
kubectl apply -f https://raw.githubusercontent.com/careerbytecode/cloud-devops-engineer-training/main/5-kubernetes_admin/6-initcontainers/node-redis/node.yml -n app1
```

- first deploy above yaml file and run below command

```
kubectl get all -n app1 -o wide
```

- you will see init is waiting.coz the dependency is not yet launched or stopped

## 3 . Create a Redis database  

```
kubectl apply -f https://raw.githubusercontent.com/careerbytecode/cloud-devops-engineer-training/main/5-kubernetes_admin/6-initcontainers/node-redis/redis.yml -n app1
```

- now immdietly riun below command

## 4 . Testing the init containers 

```
kubectl get all -n app1 -o wide
```

- you will see now running state

```
kubectl delete ns app1
```
