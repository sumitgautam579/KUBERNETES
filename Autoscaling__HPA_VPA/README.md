# Kubernetes HPA & VPA Controller (Horizontal/Vertical Pod Autoscaler) on Minikube/KIND Cluster

## In this demo, we will see how to deploy HPA controller. HPA will automatically scale the number of pods based on CPU utilization whereas VPA scales by increasing or decreasing CPU and memory resources within the existing pod containers—thus scaling capacity vertically


### Pre-requisites to implement this project:

- If you are using a Kind cluster install Metrics Server
```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
- Edit the Metrics Server Deployment
```bash
kubectl -n kube-system edit deployment metrics-server
```
- Add the security bypass to deployment under `container.args`
```bash
- --kubelet-insecure-tls
- --kubelet-preferred-address-types=InternalIP,Hostname,ExternalIP
```
- Restart the deployment
```bash
kubectl -n kube-system rollout restart deployment metrics-server
```
- Verify if the metrics server is running
```bash
kubectl get pods -n kube-system
kubectl top nodes
```
- For VPA
```bash
git clone https://github.com/kubernetes/autoscaler.git
cd autoscaler/vertical-pod-autoscaler
./hack/vpa-up.sh
```
- Verify the pods on VPA
```bash
kubectl get pods -n kube-system
```
#
## What we are going to implement:
In this demo, we will create an deployment & service files for Apache and with the help of VPA, we will automatically scale the number of pods based on CPU utilization.
#
### Steps to implement VPA:

- Update the Deployments:

  - We'll modify the existing deployment YAML files to include resource requests and limits. This is required for VPA to monitor CPU usage.
```bash

    spec:
      containers:
      - name: apache
        image: httpd:2.4
        ports:
        - containerPort: 80
        resources:
          requests:
            cpu: 100m
          limits:
            cpu: 200m

```
#
- Apply the updated deployments:
```bash
kubectl apply -f deployment.yaml
```
#
- Create HPA Resources
  - We will create HPA resources for both Apache and NGINX deployments. The HPA will scale the number of pods based on CPU utilization.
```bash
#apache-hpa.yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: apache-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: apache-deployment
  minReplicas: 1
  maxReplicas: 5
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 20
```
#
- Apply the HPA resources:
```bash
kubectl apply -f apache-hpa.yaml
```
#
- port forward to access the Apache service on browser.
```bash
kubectl port-forward svc/apache-service 8080:80 --address 0.0.0.0 &
```
#
- Verify HPA
  - You can check the status of the HPA using the following command:
```bash
kubectl get hpa
```
> This will show you the current state of the HPA, including the current and desired number of replicas.

#
### Stress Testing
#
- To see HPA in action, you can perform a stress test on your deployments. Here is an example of how to generate load on the Apache deployment using 'BusyBox':
```bash
kubectl run -i --tty load-generator --image=busybox /bin/sh
```
#
- Inside the container, use 'wget' to generate load:
```bash
while true; do wget -q -O- http://apache-service.default.svc.cluster.local; done
```

This will generate continuous load on the Apache service, causing the HPA to scale up the number of pods.

#
- Now to check if HPA worked or not, open a same new terminal and run the following command
```bash
kubectl get hpa -w
```

> Note: Wait for few minutes to get the status reflected.

#
