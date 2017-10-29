#### Networking challenges to solve:
**  **
*	container to container networking: solved by **pod** and localhost.
*	Pod to Pod communications, since pod is the smallest compute unit that kubernetes manages, it (k8) expects pod-pod communication already set up, hence pod-to-pod networking is not part of k8. Hence every pod needs to have a routable IP address.
*	External to pod - this is provided by k8 **services** 
*	Pod to services - this is covered by k8 **services**


---
The Kubernetes networking model details that each Pod should have a routable IP address. This makes communication between Pods easier by not requiring any NAT or port mappings that we had with earlier versions of Docker networking. All containers within a pod can communicate over localhost, by sharing same network namespace. For example, we can have a web server and database server placed in the same Pod and use the local interface for cross communication. As there is no additional translations performance is better to that of an NAT’d approach.

**Kube-proxy: Needed for routing external traffic to external facing PODS(mainly FE or external facing API services)**
  Kubernetes fulfills service -> Pods integration by enabling a network proxy called the kube-proxy on every node in a cluster. The network proxy is always there even if Pods are not running. Its main task is to route traffic to the correct Pod and can do TCP,UDP stream forwarding or round robin TCP,UDP forwarding. The kube-proxy captures service-destination traffic and proxies requests from the service endpoint back to the Pod running the application. The traffic is forwarded to the Pods on the target port defined in the definition file. The target port is a random port assigned during service creation. To make all this work, Kubernetes uses IPtables and Virtual IP address.

  When using Kubernetes alongside, for example, Opencontrail, the kube-proxy is disabled on all hosts, and connectivity is implemented by the OpenContrail vrouter module via overlays ( MPLS over UDP encapsulation ). Another vendor on the forefront is Midokura, the co-founder behind OpenStack Project Kuryr. This project aims to bring any SDN plugin (MidoNet, Dragon flow, OVS, etc) to Containers.

**Per POD IP: To facilitate internal communication between PODS, internal API and services**
  The Pods IP address is reachable by all other Pods and hosts in the Kubernetes cluster. The address is not usually routable outside of the cluster. This should not be too much of a concern as most traffic stays within application tiers inside the cluster. Any inbound external traffic is achieved by mapping external load-balancers to services in the cluster.

  The Pod-IP approach assumes that all Pods can reach each other without creating specific links. They can access each other by IP rather than through a port mapping on the physical host.

**Pause container:**
  Kubernetes has what’s known as a PAUSE container also referred to as a Pod infrastructure container. It handles the networking by holding the networking namespace and IP address for the containers on that Pod

---
For Pod to Pod communication, one can use tools like flannel or calico to form overlay network.
 -- Calico uses BGB to form routing mesh.
 -- Other opensource tool that can be used to implement same networking model of per pod IP are contrail/opencontrail, flannel

 If each node are assigned a sub network and with each pod gets assigned an IP from that range, that will achieve the pupose of one ip for each pod.

--
 Other network overlay tools
   -- http://www.nuagenetworks.net/
   -- https://github.com/openvswitch/ovn-kubernetes
   -- http://romana.io/
   -- https://www.weave.works/products/weave-net/  (https://www.weave.works/docs/net/latest/cni-plugin/)
   -- https://github.com/projectcalico/canal

