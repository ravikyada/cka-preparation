# Cluster Architecture & Operations

## 🎯 Exam Objectives

- understand control plane components
- node components and roles
- labels, taints, and node selection
- cluster certificates and kubeconfig
- etcd backup and restore
- cluster maintenance operations

---

## 🧩 Key Theory

### Kubernetes Control Plane

The control plane is the decision-maker of the cluster.

Components:

- **kube‑apiserver** – front door of the cluster
- **etcd** – key‑value store containing cluster state
- **kube‑scheduler** – decides which node runs a pod
- **kube‑controller‑manager** – controllers for nodes, endpoints, etc.
- **cloud‑controller‑manager** – cloud integration logic

### Node Components

- **kubelet** – manages pods on node
- **kube‑proxy** – implements Service networking
- **container runtime** – containerd, CRI‑O, etc.

---

## 🔧 Frequently Used Commands

### View cluster components
```
kubectl get componentstatuses
kubectl get nodes -o wide
kubectl describe node <name>
```

### Label nodes
```
kubectl label node node1 role=db
```

### Add taint to node
```
kubectl taint node node1 key=value:NoSchedule
```

### Remove taint
```
kubectl taint node node1 key=value:NoSchedule-
```

### Cordon / Drain / Uncordon
```
kubectl cordon node1
kubectl drain node1 --ignore-daemonsets --delete-emptydir-data
kubectl uncordon node1
```

---

## 🗄 etcd Backup & Restore

### Take backup
```
ETCDCTL_API=3 etcdctl \
 --endpoints=https://127.0.0.1:2379 \
 --cacert=/etc/kubernetes/pki/etcd/ca.crt \
 --cert=/etc/kubernetes/pki/etcd/server.crt \
 --key=/etc/kubernetes/pki/etcd/server.key \
 snapshot save /backup/snapshot.db
```

### Restore backup
```
ETCDCTL_API=3 etcdctl snapshot restore /backup/snapshot.db
```

> Exam Note: In restore questions you usually modify the **static pod manifest** to point to restored data directory.

---

## 🛠 Real‑World Scenario

Node requires kernel patch:

1. cordon node
2. drain workloads
3. patch or reboot
4. uncordon

This mirrors actual SRE workflows.

---

## 🐞 Troubleshooting Focus

- Node NotReady → check kubelet
- Pods Pending → scheduler / taints / resources
- Control plane down → check etcd and static pods
- Time not synchronized → can break cert validation

---

## ⚠️ Common Mistakes

- forgetting `--ignore-daemonsets`
- deleting pods instead of draining
- editing wrong kubeconfig context
- restoring etcd without updating manifests path

---

## 📝 Exam Tips

- static pod manifests live in `/etc/kubernetes/manifests`
- etcd default port: **2379**
- label + taint + toleration questions appear often
