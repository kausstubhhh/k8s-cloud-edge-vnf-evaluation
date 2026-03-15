# GenAI Troubleshooting Log

| Problem | Suggested Solution | Result |
|--------|--------------------|--------|
| Docker permission denied | Added user to docker group and used newgrp docker | Resolved |
| kubectl connection refused | Configured kubeconfig for K3s cluster | Resolved |
| Context conflict between Minikube and K3s | Used kubectl config use-context to switch clusters | Resolved |
| DNS testing tool selection | Used dnsperf for DNS workload benchmarking | Successful |

