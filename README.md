# Performance Evaluation of Kubernetes for Cloud and Edge Network Functions

This project evaluates the performance of a DNS-based Virtual Network Function (CoreDNS) deployed in two Kubernetes environments.

## Infrastructure

Azure VM  
Ubuntu 22.04  
2 vCPU  
4 GB RAM  

## Kubernetes Environments

Cloud environment:
Minikube Kubernetes cluster

Edge environment:
K3s lightweight Kubernetes cluster

## VNF

CoreDNS was deployed as a containerized DNS service using Kubernetes manifests.

## Experiments

DNS traffic was generated using dnsperf to measure:

- Throughput (Queries per second)
- Latency
- Packet loss

## Results

| Environment | Throughput (QPS) | Latency (ms) |
|-------------|------------------|--------------|
| Minikube | 4335 | 22.87 |
| K3s | 4211 | 22.89 |

The results show that the lightweight K3s distribution provides performance comparable to a full Kubernetes deployment.

## Repository Structure

manifests/ → Kubernetes deployment files  
workloads/ → DNS workload dataset  
experiments/ → experiment commands  
docs/ → GenAI troubleshooting documentation
