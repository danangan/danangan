# Hi, I'm Danang 👋

I build and operate cloud infrastructure, with focus on AWS, Kubernetes, and AWS. I also write code in python, javascript/typescript, and go!

## 🚀 Featured Work

### [k8s Terraform Module](https://github.com/danangan/terraform-aws-helm-k8s)

![Terraform](https://img.shields.io/badge/Terraform-7B42BC?logo=terraform&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?logo=amazonaws&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?logo=helm&logoColor=white)

This terraform module provision kubernetes cluster with batteries included:

- **Networking**: VPC and subnets set up for the cluster
- **The cluster itself**: a managed EKS control plane
- **Node groups**: CPU and GPU-based nodes for different types of workload. You'd be able to use k8s node affinity feature to deploy your workload to appropriate node.
- **Ingress**: the Kubernetes AWS ALB ingress controller
- **Container Image Repository**: a repository for storing your workload container image
- **Deployment IAM User&Role**: IAM user and role for your CI/CD workflow

Usage:
```
module "my_k8s_cluster" {
  source = "github.com/danangan/terraform-aws-helm-k8s"

  k8s_cluster_name = "my-k8s-cluster"
}
```

### [k8s Observability Stack](https://github.com/danangan/k8s-obstack)

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?logo=helm&logoColor=white)

An opinionated helm chart that provides a complete observability stacks for kubernetes application and cluster monitoring built using OpenTelemetry, Prometheus, Loki, Tempo, and Grafana. Features:

- A standardised entry point for metrics, logs and traces using the OTel collector
- Metrics, logs and traces collection for your apps running in Kubernetes
- Kubernetes cluster metrics
- Host (node) metrics
- A Grafana UI to query and explore metrics, logs and traces
- Persistent volume for the backends
- Ingress setup to expose Grafana UI

Usage:
```sh
helm install obstack oci://ghcr.io/danangan/charts/obstack --version <version>
```
