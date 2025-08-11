# Kubernetes Tutorial For Beginners

## Main k8s components

### Pod
- Smallest unit of k8s
- abstraction over container
- usually runs 1 main comtainer per pod, and then a helper container or a sidecar service that has to run inside of that pod
- each pod gets its own IP address. k8s works like a virtual network.
- each pod can communicate with each other via IP address (internal not public)
- so if i have a pod, my-app, and then another pod DB, we can communicate over IP.
- However pod compoennts in k8s are ephemeral meaning they can die very easily.

