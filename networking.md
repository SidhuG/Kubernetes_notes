#### Networking challenges to solve:
**  **
*	container to container networking: solved by **pod** and localhost.
*	Pod to Pod communications, since pod is the smallest compute unit that kubernetes manages, it (k8) expects pod-pod communication already set up, hence pod-to-pod networking is not part of k8. Hence every pod needs to have a routable IP address.
*	External to pod - this is provided by k8 **services** 
*	Pod to services - this is covered by k8 **services**
