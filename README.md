# Performance Evaluation of Kubernetes for Cloud and Edge Network Functions

This project evaluates the performance of a DNS-based Virtual Network Function (CoreDNS) deployed in two Kubernetes environments representing cloud and edge computing scenarios.

---

## Infrastructure

The experimental setup was implemented on a Microsoft Azure virtual machine with the following specifications:

- Operating System: Ubuntu 22.04  
- CPU: 2 vCPU  
- Memory: 4 GB RAM  

Both Kubernetes environments were deployed on the same virtual machine to ensure a fair and controlled comparison under identical hardware conditions.

---

## Kubernetes Environments

Two Kubernetes distributions were used:

Cloud Environment (Minikube)
- Full Kubernetes distribution  
- Represents cloud deployment scenario  

Edge Environment (K3s)
- Lightweight Kubernetes distribution  
- Optimised for edge computing  

---

## Virtual Network Function

The selected VNF is CoreDNS, deployed as a containerized DNS server using Kubernetes manifests.

The deployment includes:

- Kubernetes Deployment running the CoreDNS container  
- Kubernetes Service exposing UDP port 53  
- ConfigMap defining DNS forwarding behaviour  

---

## CoreDNS Service IP Used in Experiments

The DNS server was accessed using the ClusterIP of the Kubernetes service.

Example (K3s environment):

kubectl get svc
coredns-vnf-service   ClusterIP   10.43.202.192   53/UDP

---

## Experimental Methodology

DNS traffic was generated using the dnsperf benchmarking tool.

- Input dataset: workloads/dns_queries.txt  
- Test duration: 30 seconds per run  
- Number of runs: 3 per environment  

### Metrics Measured

- Throughput (Queries per second)  
- Average latency (ms)  
- Packet loss (%)  

---

## Experiment Command

dnsperf -s <DNS_IP> -d workloads/dns_queries.txt -l 30

---

## Results (Multi-run Evaluation)

Environment | Run 1 (QPS) | Run 2 (QPS) | Run 3 (QPS) | Average (QPS) | Avg Latency (ms) | Packet Loss
------------|------------|------------|------------|----------------|------------------|------------
Minikube (Cloud) | 4335 | 4280 | 4350 | 4321 | 22.87 | 0%
K3s (Edge) | 4211 | 4175 | 4230 | 4205 | 22.89 | 0%

The results demonstrate that K3s achieves performance very close to Minikube, with only a minor difference of approximately 2–3%, while maintaining lower system overhead.

---

## Repository Structure

k8s-vnf-performance/
├── manifests/
│   └── coredns-vnf.yaml
│       → Kubernetes Deployment, Service, and ConfigMap for CoreDNS
│
├── workloads/
│   └── dns_queries.txt
│       → DNS query dataset used for benchmarking
│
├── experiments/
│   └── commands.txt
│       → dnsperf commands and execution steps used during experiments
│
├── docs/
│   ├── COMP5123M_CW2_Q5_Results.pdf
│   │   → Performance results including tables, graphs, and analysis
│   └── GenAI_troubleshooting.md
│       → Log of issues encountered, AI-assisted solutions, and outcomes

---

## GenAI Troubleshooting Log

Problem | Suggested Solution | Result
--------|------------------|--------
Docker permission denied | Added user to docker group and used newgrp docker | Resolved
kubectl connection refused (K3s) | Configured kubeconfig using /etc/rancher/k3s/k3s.yaml | Resolved
Context conflict between Minikube and K3s | Used kubectl config use-context to switch clusters | Resolved
DNS testing tool selection | Selected dnsperf for DNS workload benchmarking | Successful
Minikube DNS not externally accessible | Exposed service using NodePort for external access | Resolved

---

## Coursework Context

This repository was developed for the module COMP5123M – Cloud Computing Systems at the University of Leeds.

The objective was to design and evaluate a cloud and edge Kubernetes architecture capable of deploying a virtual network function and measuring its performance under simulated network workloads.
