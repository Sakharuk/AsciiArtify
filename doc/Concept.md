# AsciiArtify Kubernetes Deployment Tools Evaluation

## Introduction
AsciiArtify, a startup focused on developing a new software product for transforming images into ASCII art using Machine Learning, faces the challenge of selecting the right tool for local Kubernetes cluster development. The team is considering three options: minikube, kind and k3d.

## Characteristics
### 🔹 Minikube

| Characteristic                | Description                                                                 |
|------------------------------|-----------------------------------------------------------------------------|
| **Supported OS**             | Windows, macOS, Linux                                                       |
| **Supported Architectures**  | amd64, arm64 (via Docker), arm (Raspberry Pi)                               |
| **Installation Drivers**     | Docker, VirtualBox, Hyper-V, KVM, Podman (experimental), VMware             |
| **Automation**               | ✅ CLI automation (`minikube start`, profiles, scripting)                   |
| **Monitoring Tools**         | ✅ Built-in addons: Prometheus, Metrics Server, Dashboard                   |
| **Cluster Management**       | ✅ Supports start/stop, snapshots, profiles for multiple clusters            |
| **LoadBalancer Support**     | ✅ With `minikube tunnel`                                                   |
| **Ingress Support**          | ✅ With `minikube addons enable ingress`                                    |
| **Resource Configuration**   | ✅ Configurable CPU, memory, disk                                            |
| **Cloud Emulation**          | ❌ No native cloud environment emulation                                    |

---

### 🔹 Kind (Kubernetes IN Docker)

| Characteristic                | Description                                                                 |
|------------------------------|-----------------------------------------------------------------------------|
| **Supported OS**             | Windows, macOS, Linux                                                       |
| **Supported Architectures**  | amd64, arm64                                                                |
| **Installation Drivers**     | Docker only                                                                |
| **Automation**               | ✅ High — declarative cluster config (YAML), CI/CD friendly                 |
| **Monitoring Tools**         | ❌ None built-in; must install manually (e.g., Prometheus, Grafana)         |
| **Cluster Management**       | 🟡 CLI support, but no UI or integrated dashboard                          |
| **LoadBalancer Support**     | ❌ Manual setup or MetalLB needed                                           |
| **Ingress Support**          | ❌ Manual installation (e.g., NGINX Ingress Controller)                     |
| **Resource Configuration**   | ✅ Managed via container runtime                                            |
| **Cloud Emulation**          | ❌ Focused on local development and CI use cases                            |

---

### 🔹 k3d (K3s in Docker)

| Characteristic                | Description                                                                 |
|------------------------------|-----------------------------------------------------------------------------|
| **Supported OS**             | Windows, macOS, Linux                                                       |
| **Supported Architectures**  | amd64, arm64                                                                |
| **Installation Drivers**     | Docker only                                                                |
| **Automation**               | ✅ Excellent CLI + YAML config, quick scripting                             |
| **Monitoring Tools**         | 🟡 Not built-in, but easy to add Prometheus/Grafana via Helm                |
| **Cluster Management**       | ✅ Multi-cluster support, node scaling, registry integration                |
| **LoadBalancer Support**     | ✅ Built-in (K3s has built-in service LB)                                   |
| **Ingress Support**          | ✅ Traefik ingress built-in by default                                      |
| **Resource Configuration**   | ✅ Configurable via `k3d cluster create` CLI args                           |
| **Cloud Emulation**          | ❌ Optimized for dev/test; not a full prod cluster replacement              |

## ✅ Pros and ❌ Cons

| Aspect        | **Minikube**                                                                                  | **Kind**                                                                                  | **k3d**                                                                                     |
|---------------|-----------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| **✅ Pros**    | - Full upstream Kubernetes<br>- Rich addons (Ingress, Dashboard, Prometheus)<br>- Multiple drivers (Docker, VM, Podman)<br>- Good documentation and community | - Lightweight and fast<br>- Ideal for CI/CD<br>- Pure Docker, no VM overhead<br>- YAML-based config | - Very fast and lightweight<br>- Built-in Traefik Ingress and LoadBalancer<br>- Great CLI and automation<br>- Multi-node support |
| **❌ Cons**    | - Slower startup with VM<br>- Higher resource usage<br>- Limited Podman support<br>- Not optimal for CI | - Manual Ingress and LoadBalancer setup<br>- No built-in UI<br>- No Podman support<br>- Limited production emulation | - Not full upstream Kubernetes (K3s)<br>- Fewer official addons<br>- Docker dependency<br>- Slight differences vs GKE/EKS |

## Demonstration
Recommended Tool: k3d  Deployment of "Hello World" Application on Kubernetes  

![Application on Kubernetes](demo.gif)  


## Conclusion

We recommend **k3d** as the most suitable tool for the AsciiArtify PoC due to its fast startup, low resource usage, and built-in support for Ingress and load balancing via Traefik. It offers a simple CLI, supports multi-node clusters, and is easy to automate with YAML configurations. While k3d runs on K3s (a lightweight Kubernetes variant), it is fully compatible for development and testing purposes. The only caveat is its reliance on Docker, which may need reconsideration in production. Overall, k3d strikes the best balance between speed, usability, and functionality for local Kubernetes development.
