# Hi, I'm Danang 👋

I'm a full-stack engineer working across frontend, backend, and infrastructure. I build things using JavaScript/TypeScript, Python, Go, Terraform, and AWS.

## 🚀 Featured Work

### [Knowledge Base - A RAG-powered chatbot with file management](https://github.com/danangan/knowledge-base)

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?logo=nextdotjs&logoColor=white)
![Fastify](https://img.shields.io/badge/Fastify-000000?logo=fastify&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![Haystack](https://img.shields.io/badge/Haystack-1C3D5A)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Milvus](https://img.shields.io/badge/Milvus-00A1EA?logo=milvus&logoColor=white)

A full-stack app for chatting with AI over your own documents, with saved chat history. Upload files (.pdf, .md, .txt, .docx, .xlsx) individually or in bulk from a compressed archive, and organise them into folders.

The core app is written in TypeScript (Next.js frontend, Fastify backend) and handles files and chats, with PostgreSQL for persistence. A Python retrieval service (FastAPI and Haystack) runs the RAG pipeline that embeds files into Milvus and serves the search API.

### [SaaS Core - A full-stack base for building a SaaS product](https://github.com/danangan/saas-core)

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?logo=nextdotjs&logoColor=white)
![Fastify](https://img.shields.io/badge/Fastify-000000?logo=fastify&logoColor=white)
![Jest](https://img.shields.io/badge/Jest-C21325?logo=jest&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?logo=playwright&logoColor=white)
![Testcontainers](https://img.shields.io/badge/Testcontainers-291A3F?logo=testcontainers&logoColor=white)

A base for multi-tenant SaaS products, where each company gets its own workspace (like Slack). It handles the common SaaS features so you can focus on building the actual product. Built in TypeScript with Next.js (frontend) and Fastify (backend).

It includes login and sign-up, plus a platform admin for managing companies, plans, users (including bulk invites), roles, and a company activity log. Company admins manage their own team and company name, and every user can update their profile and password or sign out everywhere.

It also comes with a complete testing setup: Jest for unit and integration tests, Testcontainers for integration test dependencies, and Playwright end-to-end tests that run against staging or local dependencies.

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
