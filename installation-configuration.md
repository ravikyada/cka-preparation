# Installation, Configuration & Upgrade

## 🎯 Exam Objectives

- install Kubernetes clusters with kubeadm
- configure networking
- bootstrap worker nodes
- upgrade clusters
- manage certificates
- manage kubeconfig

---

## 🚀 kubeadm Installation Workflow

### Initialize Control Plane
```
kubeadm init --pod-network-cidr=10.244.0.0/16
```

### Configure kubectl Access
```
mkdir -p $HOME/.kube
cp /etc/kubernetes/admin.conf $HOME/.kube/config
```

### Join Worker Nodes
```
kubeadm token create --print-join-command
```

### Install Network Plugin Example
```
kubectl apply -f <cni-plugin-file>
```

---

## 🔄 Upgrade Process (High Level)

1. drain control plane node
2. upgrade kubeadm
3. run `kubeadm upgrade apply`
4. upgrade kubelet & kubectl
5. uncordon node
6. repeat for workers

---

## 🔐 Certificates

### Check expiration
```
kubeadm certs check-expiration
```

### Renew all
```
kubeadm certs renew all
```

Certs are stored in:

```
/etc/kubernetes/pki
```

---

## ⚠️ Common Mistakes

- forgetting to drain
- forgetting network plugin after init
- mixing container runtimes
- ignoring failed pre‑flight checks

---

## 📝 Exam Tips

- memorize minimal `kubeadm init` command
- focus on logs under `/var/log/containers`
- practice configuring kubeconfig contexts
