# Performance Evaluation of Kubernetes for Cloud and Edge Network Functions

This project evaluates the performance of a DNS-based Virtual Network Function (CoreDNS) deployed in two Kubernetes environments representing cloud and edge computing scenarios.

## Infrastructure

The experimental environment was implemented on a Microsoft Azure virtual machine with the following specifications:

* Operating System: Ubuntu 22.04
* CPU: 2 vCPU
* Memory: 4 GB RAM

Both Kubernetes environments were hosted on the same VM to ensure a fair comparison using identical hardware resources.

## Kubernetes Environments

Two Kubernetes distributions were used:

**Cloud Environment**

* Minikube (full Kubernetes distribution)

**Edge Environment**

* K3s (lightweight Kubernetes distribution designed for edge computing)

## Virtual Network Function

The selected VNF is **CoreDNS**, deployed as a containerized DNS server using Kubernetes manifests.

The deployment consists of:

* Kubernetes Deployment running the CoreDNS container
* Kubernetes Service exposing UDP port **53**
* ConfigMap containing the DNS configuration

## CoreDNS Service IPs Used in Experiments

The DNS server inside each cluster was accessed using the Kubernetes **ClusterIP** of the CoreDNS service.

Example service output:

```
kubectl get svc
```

Edge environment (K3s):

```
coredns-vnf-service   ClusterIP   10.43.202.192   53/UDP
```

This IP address was used as the DNS target for the performance experiments.

## Experimental Methodology

DNS traffic was generated using the **dnsperf** benchmarking tool.

A dataset of DNS queries located in the `workloads` directory was used as the workload input.

Performance was measured using the following metrics:

* Throughput (Queries per second)
* Average response latency
* Packet loss

## Experiment Command

Example command used during the experiments:

```
dnsperf -s 10.43.202.192 -d dns_queries.txt -l 30
```

Where:

* `-s` specifies the DNS server IP
* `-d` specifies the query dataset
* `-l 30` runs the test for 30 seconds

## Results

| Environment      | Throughput (QPS) | Avg Latency (ms) | Packet Loss |
| ---------------- | ---------------- | ---------------- | ----------- |
| Minikube (Cloud) | 4335             | 22.87            | 0%          |
| K3s (Edge)       | 4211             | 22.89            | 0%          |

The results show that the lightweight **K3s** distribution provides performance very close to the full Kubernetes environment while using fewer system resources.

## Repository Structure

```
manifests/    Kubernetes deployment files
workloads/    DNS query dataset used for experiments
experiments/  Commands used to run dnsperf benchmarks
docs/         GenAI troubleshooting log and experiment documentation
```

## Coursework Context

This repository was created for the module **COMP5123M – Cloud Computing Systems** at the University of Leeds.
The objective was to design and evaluate a cloud and edge Kubernetes architecture capable of running a virtual network function and measuring its performance under simulated network workloads.
