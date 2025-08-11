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
- even if the pod dies, no worry about IP changing

### App should be accessible through browser
- for this you need to create an external service
- service that opens communication from external sources.
- don't want DB to be open to the public requests
- create an internal service for DB
- url of external service isn't very practical http://nodeIP:port
- k8s has Ingress to forward better looking names like https://my-app.com to the correct IP:port
- this prob works a lot like DNS

### ConfigMap and Secret
- pods communicate with each other using a, where do you configure endpoint?
- usually database url is in the built application.
- usually you would have to re-build application with new version and then push to repo and now you have to pull that new image in your pod and restart the whole thing
- very tedious for a small change like database url.
- ConfigMap will contains URLs of a database or some other services that use it. and in kubernetes you just connect it to the pod so that the pod gets the data that ConfigMap contains.
- and now if you change the name of the service the endpoint is just involving adjusting configmap, no need to build a new image and go through a long cycle
- username and password may change and putting this in a configmap is insecure even though its an external config.
- for this reason there is another configuration by k8s called Secret which is used to store secret data - stored in a base64 encoded format
- secret would contain things like credentials.
