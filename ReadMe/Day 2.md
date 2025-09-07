### Day 2 – Creating AKS and Connecting via Cloud Shell

- **Subscription:** Using default Azure subscription  
- **Resource Group:** Created `Portfolio-Kubernetes-rg`  
- **Cluster Configuration:** Selected **Dev/Test** configuration  
- **Cluster Name:** `Portfolio_Cluster`  
- **Region:** Canada Central  
- **Pricing Tier:** Free  
- **Node Size:** Standard D2pls v6 (2 vCPUs, 4 GiB memory)  
- Left other settings as default and created the cluster  

---

#### 🔗 Connecting to AKS via Cloud Shell

After the cluster was created, I used **Azure Cloud Shell (Bash)** to connect to the cluster and verify it.  

⚡ **Commands Used (with explanations):**

#### 👉 Tells Azure CLI which subscription to use (important if you have multiple subscriptions).
This ensures that all further commands are run under the correct subscription.
```bash
az account set --subscription 970a2be3-c5af-459d-b1c4-9f2acdc965c1
```
#### 👉 Downloads the Kubernetes credentials for the AKS cluster and merges them into your local configuration file (.kube/config).
This allows you to use kubectl commands to talk directly to your AKS cluster.
Think of this as “logging in” to your cluster.

```bash 
az aks get-credentials --resource-group Portfolio-Kubernetes-rg --name Portfolio_Cluster --overwrite-existing
```

#### 👉 Shows both client version (your local kubectl) and server version (the Kubernetes version running on your AKS cluster).
This helps confirm that your cluster is up and responding.

```bash
bashkubectl version
```

#### 👉 Lists the nodes (virtual machines) that your AKS cluster is running on.
Each node is a worker machine where your applications/containers will run.


```bash 
kubectl get nodes
```




Output example:
```
NAME                                STATUS   ROLES    AGE   VERSION
aks-agentpool-15830584-vmss000000   Ready    <none>   19h   v1.32.6
```

✅ Status = "Ready" → Your cluster node is healthy and ready to run workloads.

```bash
kubectl get nodes -o wide
```
#### 👉 Same as above, but with more details like internal IP, OS image, kernel version, and container runtime.
This is useful for troubleshooting and cluster insights.



Output example:
```
NAME                                STATUS   ROLES    AGE   VERSION   INTERNAL-IP   EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
aks-agentpool-15830584-vmss000000   Ready    <none>   19h   v1.32.6   10.224.0.4    <none>        Ubuntu 22.04.5 LTS   5.15.0-1092-azure   containerd://1.7.27-1
```

