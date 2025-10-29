# Setting Up a Multi Node Local Kubernetes Cluster Using Kind (Kubernetes IN Docker)

A lot of people might asked me which **cloud provider** we’ll be using for this entire Kubernetes (CKA) series.  
My answer: **none of them** — at least, not yet.

Before we jump into managed Kubernetes services like **AKS**, **EKS**, or **GKE**, it’s essential to **understand Kubernetes itself** — by installing and running it **locally**.  
This approach gives you **maximum learning and hands-on experience**, which is crucial for both mastering Kubernetes and preparing for certifications like **CKA**.

---

## 🧠 Why Local Installation?

Managed services (like EKS or GKE) hide most of the complexity — for example, you won’t even get access to the **control plane node**.  
That means you can’t troubleshoot key components or fully understand what’s happening under the hood.

So in this tutorial, we’ll install Kubernetes **locally** using **Kind**.

---

## 🔧 What is Kind?

**Kind** stands for **Kubernetes IN Docker**.  
It’s one of the most popular tools to create a local Kubernetes cluster using Docker containers as nodes.  

In simple terms:
- Each Docker container acts as a **node**.
- These nodes can be either **control plane** or **worker nodes**.
- The setup is lightweight, fast, and perfect for learning.

<!-- ![Kind Overview](./assets/page-1.jpg) -->

---

## 🧩 Prerequisites

Before installing Kind, ensure you have:

- **Go** version `>= 1.16`
- **Docker**, **Podman**, or **nerdctl** installed (Docker is recommended and already covered in a previous prerequisite tutorial)

---

## ⚙️ Installing Kind

Head over to the [official Kind documentation](https://kind.sigs.k8s.io/docs/user/quick-start/) for installation options.

You can install Kind via:
- **Package Manager**
- **Release Binaries**
- **Source Installation**

We’ll use the **package manager** method.

### For macOS:
```bash
brew install kind
````

### For Windows:

```bash
choco install kind
```

### For Linux:

You can follow the instructions from the release binaries section on the Kind page.

Once installed, verify by running:

```bash
kind version
```

---

## 🚀 Creating Your First Kubernetes Cluster

To create a local cluster, run:

```bash
kind create cluster
```

This will:

* Pull the default Kubernetes image,
* Spin up Docker containers (nodes),
* Initialize your control plane and worker nodes.

By default, the cluster name will be **kind**.

If you want to specify a version and custom name:

```bash
kind create cluster \
  --name cka-cluster1 \
  --image kindest/node:v1.29.4
```

![Create Cluster](./assets/page-2.jpg)

✅ **Tip:**
If you’re preparing for the CKA exam, use the same Kubernetes version mentioned in the CNCF exam guide (e.g., `v1.29.x` as of May 2024).

---

## 🧾 Verifying the Cluster

Once created, check cluster info:

```bash
kubectl cluster-info --context kind-cka-cluster1
```

Example output:

```
Kubernetes control plane is running at https://127.0.0.1:63787
CoreDNS is running at kubernetes-dashboard/kube-system
```

![Check Cluster Info](./assets/page-3.jpg)

---

## ⚒️ Installing kubectl (if not installed)

`kubectl` is the **CLI tool** used to interact with any Kubernetes cluster — whether local, on-prem, or cloud-managed.

To install it:

### Linux:

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

### macOS:

```bash
brew install kubectl
```

### Windows:

```bash
choco install kubernetes-cli
```

Verify installation:

```bash
kubectl version --client
```

---

## 🧭 Checking Nodes

Now that your cluster is up, let’s check the nodes:

```bash
kubectl get nodes
```

Example output:

```
NAME                         STATUS   ROLES           AGE     VERSION
cka-cluster1-control-plane   Ready    control-plane   5m53s   v1.29.4
```

Currently, it’s a **single-node cluster** (control plane + worker combined).

---

## 🧱 Creating a Multi-Node Cluster

In a real setup, you’d want **separate nodes** for the control plane and workers.

Kind allows that using a simple **configuration YAML**.

Create a file named `config.yml`:

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```

Now run:

```bash
kind create cluster \
  --name cka-cluster2 \
  --config config.yml \
  --image kindest/node:v1.29.4
```

![Multi-Node Cluster](./assets/page-4.jpg)

Check the nodes:

```bash
kubectl get nodes
```

Expected output:

```
NAME                         STATUS   ROLES           AGE     VERSION
cka-cluster2-control-plane   Ready    control-plane   2m23s   v1.29.4
cka-cluster2-worker          Ready    <none>          2m1s    v1.29.4
cka-cluster2-worker2         Ready    <none>          2m2s    v1.29.4
```

---

## 🔄 Switching Between Multiple Clusters

If you have multiple clusters (e.g., `cka-cluster1` and `cka-cluster2`), check available contexts:

```bash
kubectl config get-contexts
```

You’ll see something like:

```
CURRENT   NAME                CLUSTER             AUTHINFO            NAMESPACE
          kind-cka-cluster1   kind-cka-cluster1   kind-cka-cluster1   
*         kind-cka-cluster2   kind-cka-cluster2   kind-cka-cluster2
```

The asterisk `*` marks the **current active context**.

To switch between clusters:

```bash
kubectl config use-context kind-cka-cluster1
```

![Switch Contexts](./assets/page-5.jpg)

---

## 💡 Exam Tip

In the **CKA exam**, you’ll be required to switch between clusters frequently.
Each question specifies which context to use — make sure to switch **before performing any task**, or your answer won’t be graded correctly.

Command:

```bash
kubectl config use-context <context-name>
```

---

## 🧭 Useful Resources

Here are some resources you can refer to (and even use during the exam):

* [Kubernetes Documentation](https://kubernetes.io/docs/)
* [Kubernetes Blog](https://kubernetes.io/blog/)
* [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

Make sure to **practice enough** so you don’t need to look up commands during the exam — it’ll save you valuable time.

---

## 🏁 Summary

In this tutorial, you learned how to:

* Install **Kind** (Kubernetes in Docker)
* Create a **local Kubernetes cluster**
* Verify and manage **nodes**
* Create a **multi-node setup**
* Switch between **multiple clusters**
* Understand **kubectl context management**

In the **next post**, we’ll dive into:

* Creating your **first Pod**
* Understanding **imperative vs. declarative** approaches
* Learning the basics of **YAML**

---