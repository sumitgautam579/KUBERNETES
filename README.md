 #   Kubernetes on AWS EC2

A guide and toolkit for quickly provisioning and configuring a Kubernetes cluster on AWS EC2 instances using Kind and Docker.

## Defining workload using YAML

Help us to understand the use of different YAML files for the creation of pods and namespaces.
### Deployments

1. `kubectl apply -f deployment.yml`  
   Deploy a workload defined in `deployment.yml`.
2. `kubectl scale deployment nginx-deployment --replicas=3 -n nginx`  
   Scale the deployment to 3 replicas.

### StatefulSets

1. `kubectl apply -f statefulset.yml`  
   Deploy a StatefulSet defined in `statefulset.yml`.
2. `kubectl describe statefulset mysql -n database`  
   Display detailed information about a StatefulSet.

### DaemonSets

1. `kubectl apply -f daemonset.yml`  
   Deploy a DaemonSet for running pods on every node.
2. `kubectl describe daemonset fluentd -n logging`  
   Display details about a DaemonSet.

### ReplicaSets

1. `kubectl apply -f replicaset.yml`  
   Deploy a ReplicaSet for managing pod replicas.
2. `kubectl describe replicaset nginx-replicaset -n nginx`  
   Show detailed information about the ReplicaSet.
---


