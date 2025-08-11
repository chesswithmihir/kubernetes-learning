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
  - node can crash
  - kubelet can restart
- and so when this happens a new pod can get created --> new ip address which is inconvenient for communicating to DB pod or any pod via IP because IPs keep swapping as a part of fault tolerance
- another component of k8s is used instead of IP called Service because of this

### Service and Ingress
- Service: permanent IP address that can be attached to each pod.
- my-app can have its own service
- db pod can have its own service
- lifecycle of Pod and Service Not connected

