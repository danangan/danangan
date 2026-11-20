# Hi, I'm Danang 👋

I'm a full-stack engineer working across frontend, backend, and infrastructure. I build things using Javascript/Typescript, Python, Go, Terraform, AWS.

## 🚀 Featured Work

### [SaaS Core - A full-stack base for building a SaaS product](https://github.com/danangan/saas-core)

A base for multi-tenant SaaS products. Each company is its own workspace (like Slack). This projects handle the base SaaS features that you can build on top on so you can focus on building the actual product. Built in Typescript using Next.js (frontend) and Fastify (backend).

Features:
- Authentication
  - Log in
  - Account creation
- Platform admin
  - Company management: create, rename, activate or deactivate, delete, change the plan
  - User management: invite users, one at a time or in bulk
  - Role management: company admin or member
  - Company activity log
- User admin
  - Manage the team: invite, edit, change roles, deactivate, delete
  - Rename the company
- All user
  - Settings: personal info, change password, sign out everywhere
 
This project also provides you with complete testing setup:
  - unit test and integration test runner using jest
  - integration test libraries using testcontainers
  - end2end test setup using playwright
    - staging mode
    - local mode where you can run end2end test against a local dependency, useful for local development

### [LLM Deployment to k8s](https://github.com/danangan/diy-llm)

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?logo=helm&logoColor=white)

An experimental DIY project to deploy an open-source LLM to AWS EKS, using vLLM as the runtime. It uses my other two projects below as the main building blocks for its infrastructure and observability setup:

- **Infrastructure**: the EKS cluster is provisioned with [terraform-aws-helm-k8s](#aws-eks-k8s-terraform-module), and the LLM runs as a container using S3 as model storage.
- **Observability**: monitoring is provided by [k8s-obstack](#k8s-observability-stack-obstack), with vLLM's traces and metrics wired in so they're visible in Grafana.

### [AWS EKS k8s Terraform Module](https://github.com/danangan/terraform-aws-helm-k8s)

![Terraform](https://img.shields.io/badge/Terraform-7B42BC?logo=terraform&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?logo=amazonaws&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?logo=helm&logoColor=white)

This Terraform module provisions a Kubernetes cluster with batteries included:

- **Networking**: VPC and subnets set up for the cluster
- **The cluster itself**: a managed EKS control plane
- **Node groups**: CPU and GPU-based nodes for different types of workloads
- **Ingress**: the AWS Load Balancer Controller for Kubernetes ingress
- **Container image repository**: a repository for storing your workload container images
- **Persistence**: EBS and EFS-based persistence for your workloads
- (Optional) [Cilium](https://github.com/danangan/terraform-aws-helm-k8s#cilium) as the CNI instead of the VPC CNI and kube-proxy
- (Optional) [EKS Auto Mode](https://github.com/danangan/terraform-aws-helm-k8s#eks-auto-mode) if you prefer EKS to manage the nodes, ingress, and storage itself

This module is perfect for spinning up a k8s cluster for a small project where you want tight control over your compute resources (for cost-control purposes). Otherwise, you can always enable EKS Auto Mode.

Usage:
```hcl
module "my_k8s_cluster" {
  source = "github.com/danangan/terraform-aws-helm-k8s"

  cluster_name = "my-k8s-cluster"
}
```

### [k8s Observability Stack (obstack)](https://github.com/danangan/k8s-obstack)

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?logo=helm&logoColor=white)

An opinionated Helm chart that provides a complete observability stack for Kubernetes application and cluster monitoring, built with OpenTelemetry, Prometheus, Loki, Tempo, and Grafana.

Features:

- A standardised entry point for metrics, logs, and traces using the OTel Collector
- Metrics, logs, and traces collection for your apps running in Kubernetes
- Kubernetes cluster metrics
- Host (node) metrics, including GPU metrics (NVIDIA only)
- A Grafana UI to query and explore metrics, logs, and traces
- Persistent volumes for the backends
- Ingress setup to expose the Grafana UI

Usage:
```sh
helm install obstack oci://ghcr.io/danangan/charts/obstack --version <version>
```
