## Kubernetes: Overview and Features

**Kubernetes** is an open-source platform designed to automate the deployment, scaling, and operation of application containers. It helps manage applications that consist of hundreds or thousands of containers across various environments.

### Problems Kubernetes Solves:

- **Transition from Monolithic to Microservices:** With the rise of microservices and increased usage of containers, there’s a need for efficient container orchestration.
  
### Key Features Offered by Kubernetes:

- **High Availability:** Ensures minimal or no downtime for applications.
- **Scalability:** Supports high performance by easily scaling applications.
- **Disaster Recovery:** Provides mechanisms for recovering from failures.

### Kubernetes Components:

1. **Node:**
   - A physical server or a virtual machine that runs Kubernetes.

2. **Pod:**
   - A small unit in Kubernetes that acts as an abstraction layer over containers, creating a running environment.
   - Multiple containers can run inside one pod, but usually, there is one pod per application.
   - Each pod has its own IP address and is ephemeral, meaning it can be recreated with a new IP address.

3. **Service:**
   - Provides a permanent IP address that can be attached to pods.
   - Includes load balancing capabilities.
   - The lifecycle of pods and services are independent.
   - **External Service:** Exposes pods to the external network.
   - **Internal Service:** Does not expose pods to public requests.

4. **Ingress:**
   - Acts like a domain name service, routing URLs to specific IP addresses.

5. **ConfigMap:**
   - Stores external configuration data such as database URLs, usernames, and passwords. 
   - Note: Credentials should not be stored in ConfigMaps.

6. **Secret:**
   - Similar to ConfigMap, but used for storing sensitive data (e.g., credentials) encoded in base64.

7. **Volume:**
   - Provides persistent storage by attaching a physical hard drive, which can be local or remote.
   - Kubernetes does not manage the data on the volume.

### Deployment and Stateful Sets:

- **Deployment:**
  - Used for stateless applications.
  - Defines a blueprint specifying the number of replicas (pods) you want.
  - Deployments are an abstraction of pods and allow for easy scaling and management.

- **StatefulSet:**
  - Used for stateful applications like databases.
  - Ensures that stateful data remains consistent across replicas, but is more complex to manage compared to deployments.

### Kubernetes Architecture:

1. **Node Process (Worker Machine):**
   - Each node runs multiple pods.
   - Key processes on each node:
     - **Container Runtime:** E.g., Docker, to run containers.
     - **Kubelet:** Manages pods and ensures containers are running as expected.
     - **Kube Proxy:** Handles networking and communication between nodes.

2. **Master Process:**
   - Key processes on each master node:
     - **API Server:** Acts as the gateway and gatekeeper, handling authentication and request validation.
     - **Scheduler:** Determines on which node a pod should be deployed.
     - **Controller Manager:** Monitors the state of the cluster and makes adjustments (e.g., restarting pods) as needed.
     - **etcd:** A distributed key-value store that serves as the "brain" of the cluster, persisting all cluster state and configuration.

   - **Multiple Masters:** In a highly available setup, multiple master nodes run these processes, with etcd distributed across them.

### Example Basic Cluster Setup:
- 2 master nodes
- 3 worker nodes

### Tools and Utilities:

- **Minikube:**
  - A tool that creates a virtual Kubernetes cluster on your local machine for testing purposes.
  - It typically consists of one node running both the master and worker processes.

- **Kubectl:**
  - A command-line tool to interact with Kubernetes clusters (e.g., Minikube, cloud-based clusters).
  - Communicates with the API server running on the master node.
  
  - need a blueprint to create a pod
  
  - Don't need to handle replicasset only deployment therfore when you update configuration fiie or edit deployement  everything below that gonna be updated
  
  
 ### Minikube and kubectl Commands:

- **`minikube start`**
  - Starts a local Kubernetes cluster using Minikube. This command sets up a virtual machine with Kubernetes running on it.

- **`kubectl get nodes`**
  - Lists all the nodes in the Kubernetes cluster. This command shows the status and details of each node.

- **`sudo snap install kubectl`**
  - Installs the `kubectl` command-line tool using Snap. This is a package management system for Linux.

- **`sudo snap install kubectl --classic`**
  - Installs `kubectl` with classic confinement, allowing it to have more access to the system.

- **`kubectl get nodes`**
  - Repeats the command to list nodes, ensuring `kubectl` is properly installed and can interact with the cluster.

- **`kubectl get pods`**
  - Lists all pods running in the cluster. This command helps to see the status of all containers.

- **`kubectl get services`**
  - Lists all services in the cluster. This command provides information on how services are exposed and their status.

- **`kubectl create -h`**
  - Displays the help documentation for the `kubectl create` command, showing how to use it and its options.

- **`kubectl create deployment nginx-deploy --image=nginx`**
  - Creates a new deployment named `nginx-deploy` with an `nginx` container. This command sets up a new instance of the Nginx web server.

- **`kubectl get deployments`**
  - Lists all deployments in the cluster, showing their status and configuration.

- **`kubectl create deployment mongo-deploy --image=mongo`**
  - Creates a new deployment named `mongo-deploy` with a `mongo` container. This sets up an instance of MongoDB.

- **`kubectl describe pod mongo-deploy-7cfc5fcd78-r2bhr`**
  - Shows detailed information about a specific pod. Replace `mongo-deploy-7cfc5fcd78-r2bhr` with the actual pod name to get its details.

- **`kubectl exec -it mongo-deploy-7cfc5fcd78-r2bhr -- /bin/bash`**
  - Opens an interactive terminal session within the specified pod. Replace `mongo-deploy-7cfc5fcd78-r2bhr` with the actual pod name.

- **`kubectl delete deployment mongo-deploy`**
  - Deletes the deployment named `mongo-deploy`. This removes the associated pods and other resources created by the deployment.

- **`kubectl get replicaset`**
  - Lists all ReplicaSets in the cluster. ReplicaSets ensure that a specified number of pod replicas are running at any given time.

- **`kubectl apply -f nginx-deployment.yaml`**
apply command is used to apply the configuration file to the cluster
 

### Configuration file for deploymentgit

- Every configuration file for deployment should have 3 parts metadata, spec and status . Status is filled by kubernetes
 itself

- Connection is established by using label and selector. Label is declared in metadata and selector is declared in spec

- Labels are key value pairs. And is used to identify the resources

- Selector is used to select the resources 
