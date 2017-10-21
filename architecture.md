**Components**
1.    Master Node (central manager)
    Master node runs following services
    *    API Server - source of truth on state of the k8 cluster to the outside world, including kubectl. 
    *    Scheduler - finds the worker node to run the container.
    *    Controller manager - responsible for maintaing state of the K8 cluster, reconcile the actual state of the cluster with desired state.. 
2. Worker Nodes
    Each worker node runs following processes
    * Kubelet - recieves request from master to run containers and watches them on the local worker node.
    * Service Proxy - responsible for exposing container on the network.
3. etcd
    etcd form the central key value store, where the state of the Kubernetes cluster is kept. etcd itself runs as a cluster. API server is the one that reads/writes data to etcd. All other services running either on master or worker nodes use API to query and update state of containers.

Each of the above services can run as seperate processes on a node or as a containers themselves.
