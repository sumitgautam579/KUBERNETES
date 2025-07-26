# Kubernetes for Beginners 🐳

Welcome to your hands-on Kubernetes learning playground! This repository contains step-by-step guides and example manifests to master core Kubernetes concepts, from local cluster setup to advanced features like autoscaling and custom resources.

---

## 📂 Repository Structure

```plaintext
KUBERNETES/                          # Root directory
├── assets/                      
├── KIND_CLUSTER/                    # Kind cluster configuration and manifests
├── Practice_K8s_using_Kind.md       # Guided exercises for Kind-based clusters
├── Ubuntu_minikube_installation.md  # Minikube setup instructions on Ubuntu
├── Windows_Installation_Minikube.md # Minikube setup instructions on Windows
├── apache/                          # Apache HTTPD deployment examples
├── NGINX/                           # NGINX Deployment & Service samples
├── mysql/                           # MySQL StatefulSet and Service demos
├── helm/                            # Helm chart tutorials and examples
├── monitoring_K8s/                  # Prometheus & Grafana monitoring manifests
├── CustomResourceDefinations/       # CustomResourceDefinition examples
├── Autoscaling__HPA_VPA/            # Horizontal & Vertical Pod Autoscaler demos
├── to-do-notes-app/                 # Sample To-Do application deployment
└── README.md                        # ← You are here
```

---

## 🔧 Prerequisites

- **Docker** (for Minikube & Kind drivers)
- **kubectl** CLI (v1.21+)
- **Minikube** (v1.20+)
- **Kind** (v0.11+)
- **Helm** (v3+)

---

## 🚀 Quick Start

1. **Clone the repo**

   ```bash
   git clone https://github.com/sumitgautam579/KUBERNETES.git
   cd KUBERNETES
   ```

2. **Choose your local cluster**

   - **Minikube (Ubuntu)**:
     ```bash
     # See Ubuntu_minikube_installation.md for details
     minikube start --driver=docker
     ```
   - **Minikube (Windows)**:
     ```powershell
     # See Windows_Installation_Minikube.md for details
     minikube start --driver=hyperv
     ```
   - **Kind**:
     ```bash
     # See Practice_K8s_using_Kind.md for exercises
     kind create cluster --config KIND_CLUSTER/config.yaml
     ```

3. **Deploy examples** Navigate into any example folder and apply the manifests:

   ```bash
   kubectl apply -f apache/
   kubectl apply -f NGINX/
   kubectl apply -f mysql/
   ```

4. **Explore advanced features**

   - Autoscaling: `kubectl apply -f Autoscaling__HPA_VPA/`
   - CRDs: `kubectl apply -f CustomResourceDefinations/`
   - Monitoring: `kubectl apply -f monitoring_K8s/`
   - Helm charts: `helm install myapp helm/my-chart`

---

## 📖 Learning Pathway

1. **Cluster Setup**: Follow OS-specific guides in `*minikube_installation.md`.
2. **Core Concepts**: Practice with `apache/`, `NGINX/`, and `mysql/` folders.
3. **Helm & Advanced**: Dive into `helm/`, `Autoscaling__HPA_VPA/`, and `CustomResourceDefinations/`.
4. **Monitoring & Logging**: Experiment in `monitoring_K8s/`.

---

## 💡 Tips

- Use `kubectl logs`, `kubectl describe`, and `kubectl get events` to debug.
- Combine `kubectl port-forward` with your local browser for service access.
- Clean up resources:
  ```bash
  kubectl delete -f <folder>/ --all
  ```

---

## 🤝 Contributing

Feel free to submit issues or pull requests—add new examples, fix typos, or improve docs. Contributions are always welcome!

---

## 📄 License

@copyright *Sumit Gautam DEVOPS_Engineer*

