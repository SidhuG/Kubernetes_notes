## CNI, Container Networking Interface
---
 CNI is a specification and collection of associated libraries to write plugins that configures container networking. It's goal is to provide common interface between various networking solutions and container runtimes.
---
Kubernetes uses CNI plug-ins to orchestrate networking. Everytime a POD is initialized or removed, the default CNI-plugin is called with default configuration and that creates a pseudo interface, attaches it to the underlay network, sets IP and routes and maps it to the POD namespace. However kubernetes supports only one CNI interface per POD with one cluster wide configuration. Hence one can have only one interface per pod and can use only one overlay solution within cluster.