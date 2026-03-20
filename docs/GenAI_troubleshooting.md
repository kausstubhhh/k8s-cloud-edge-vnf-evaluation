# GenAI Troubleshooting Log
| Problem                                   | Suggested Solution                                                                  | Result     |
| ----------------------------------------- | ----------------------------------------------------------------------------------- | ---------- |
| Docker permission denied                  | Added user to docker group and reloaded group using `newgrp docker`                 | Resolved   |
| kubectl connection refused (K3s)          | Configured kubeconfig using `/etc/rancher/k3s/k3s.yaml` and set correct permissions | Resolved   |
| Context conflict between Minikube and K3s | Used `kubectl config use-context` to switch between clusters                        | Resolved   |
| DNS testing tool selection                | Selected `dnsperf` for realistic DNS workload benchmarking                          | Successful |
| Minikube DNS not externally accessible    | Exposed service using NodePort to enable external DNS testing via dnsperf           | Resolved   |

