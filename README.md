# Run Jenkins on a Kubernetes Cluster

A Kubernetes Deployment for Jenkins 2.3 for Google Container Engine with support for Github Deploy Keys (via kubernetes secret). To install into the default cluster:

```
chmod o+x setup.sh
./setup.sh
```

The public key to use as deploy key is output to the terminal.

Find out the IP of the service (it may take a minute until the load balancer has been provisioned, wait for a bit before running):
```
kubectl get servicesonpath={.status.loadBalancer.ingress[0].ip}
``` 

Navigate to the URL to setup Jenkins. The password for the installation can be obtained like this:
```
kubectl exec $(kubectl get pods -l name=jenkins -o jsonpath={.items[0].metadata.name}) cat /var/jenkins_home/secrets/initialAdminPassword
``` 
