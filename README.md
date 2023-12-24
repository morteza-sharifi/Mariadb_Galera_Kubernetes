Translation to English, ensuring accurate technical terms:

---

### MariaDB Galera Cluster on Kubernetes

- **Description**: Utilizing MariaDB Galera Cluster in Kubernetes brings significant benefits, making it a superior choice for production environments:

  1. **Scalability and Flexibility**: Ability to increase or decrease resources based on operational needs.
  2. **High Availability**: Fault detection and automatic recovery systems to maintain database stability and continuous access.
  3. **Operational Automation**: Facilitates cluster management, deployment, and scaling automatically.
  4. **Enhanced Security**: Use of namespaces and access policies to boost data security.
  5. **Ease of Management**: A powerful and straightforward user interface for more efficient management.

These advantages make MariaDB Galera Cluster in Kubernetes an optimal choice for organizations seeking scalable and robust solutions for their data management.

### Prerequisites

To use this project, the following are required:

1. **Kubernetes Cluster**: Access to an active Kubernetes cluster.
2. **kubectl Installation**: The kubectl tool must be installed on your system.
3. **Basic Kubernetes Knowledge**: Familiarity with basic concepts and operations in Kubernetes.

### Usage

1. **Cloning the Repository**:
   - To start, clone the repository with the following command:
     ```
     git clone https://github.com/morteza-sharifi/mariadb_galera_kubernetes.git
     cd mariadb_galera_kubernetes
     ```

2. **File Descriptions**:
   - Brief description of each YAML file:
     - `mariadb_node1.yaml`, `mariadb_node2.yaml`, ...: These files are for deployment. You can create as many as needed by changing the node number. Note that only node 1 is different, as its role is to establish the primary cluster.
     - `mariadb_node1svc.yaml`, `mariadb_node2svc.yaml`, ...: These services connect directly to their respective nodes and are used in the configmap. **To ultimately use the main service, you should create your own service and distinguish all deployments with a unique label.**
     - `mariadb_node1-configmap.yaml`, `mariadb_node2-configmap.yaml`, ...: No changes are needed unless you want to increase or decrease the number of databases. For an increase, changes in the **60-galera.cnf** file must be applied to all nodes, and the names of other services should be added to the `wsrep_cluster_address` variable.
     - `mariadb_node1pvc.yaml`, `mariadb_node2pvc.yaml`, ...: If you want to add databases, a Persistent Volume Claim (PVC) must be created for each node.

3. **Execution Instructions**:
   ```
   for i in $(echo $(ls deployment/)) ; do kubectl apply -f deployment/$i -n {NAMESPACE}; echo $i; done
   ```

### Important Notes

- "This is an initial version that I have prepared, suitable for operational use. As long as none of the MariaDB nodes are removed from the cluster, you will generally not encounter any issues. However, if you intend to re-add a MariaDB node that was previously removed from the cluster, it will be necessary to perform manual configurations. I am working on resolving this issue, but it is important to be aware of this limitation."
---# Mariadb_Galera_Kubernetes
