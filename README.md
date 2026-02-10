# FortiCNAPP + Dynatrace Demo Guide README Demo

## Demo Goal
Show how **FortiCNAPP** (cloud-native security) and **Dynatrace** (full-stack observability) work together to give **complete visibility** into cloud-native workloads.

- **FortiCNAPP:** Detects vulnerabilities, misconfigurations, compliance issues, and threats.
- **Dynatrace:** Monitors application performance, traces, metrics, logs, and AI-driven anomaly detection.

**Demo message:**  
“See problems before they become incidents—both security and performance—across your cloud workloads.”

---

## Demo Env 
- **Workload:** Kubernetes cluster running a sample container app (OWASP Juicy Shop)
- **FortiCNAPP:** Scans containers and workloads via agent or API connector.
- **Dynatrace:** One agent per node/container to show metrics, traces, and AI problem detection.

## Demo Architecture

- **Workload:** Kubernetes cluster (can be OpenShift or EKS) with a sample app (like a microservices demo or e-commerce app).

- **FortiCNAPP:** Integrated via agent (for CWPP) or API connector. Will show:
  - Vulnerabilities per container/service
  - Misconfigurations
  - Compliance dashboard (CIS benchmark)

- **Dynatrace:** One agent per node/container, showing:
  - Transaction tracing
  - Metrics and logs
  - AI-detected anomalies

**Outcomes**  
1. FortiCNAPP detects security risk.  
2. Dynatrace shows performance degradation.  
3. Teams can prioritize fixes with **risk + impact context**.

---

## Container JS

**OWASP Juice Shop** – purposely insecure web app

```bash
docker run --rm -p 3000:3000 bkimminich/juice-shop

- Running container as Root
securityContext:
  runAsRoot: true

- Running CPU Stress test 
apt-get update && apt-get install -y stress
stress --cpu 2 --timeout 30

- Running Memory Stress test 
stress --vm 1 --vm-bytes 200M --timeout 30

- Running Loading test
ab -n 1000 -c 50 http://<container-ip>:3000/
