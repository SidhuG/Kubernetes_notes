**What challenges does Kubernetes solve?**
kubernetes addresses challenges of scheduling containers, connecting containers running on multiple hosts, scalling them when needed, service discovery, deploying applications without downtime.
To address those challenges above, it uses its own primitives and very powerful API.

***
**what is required to containerize an application?**
To containerize an existing monolith application, one needs to:
1. Re-architect a distirbuted application based on microservices designs.
2. Build core infrastructure for running of these services
3. Build a continous integration pipeline to build container images safely and securely, test them, verify them, ready to deploy them.
4. Able to do rolling deploy, blue/green deployment, canary deployment.
5. Monitoring of containers/microservices and reporting.
6. Self discovery and Self healing should be in place.  
***
