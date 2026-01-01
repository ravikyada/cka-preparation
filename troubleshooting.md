# Troubleshooting Kubernetes

## 🎯 Exam Objectives

- debug failing pods
- network issues
- node failure
- control plane failure
- application logs

---

## 🛠 Key Commands

```
kubectl logs pod
kubectl describe pod
kubectl get events --sort-by=.metadata.creationTimestamp
```

### Debug into container

```
kubectl exec -it pod -- sh
```

### Check node status
```
kubectl get nodes
```

---

## 🧨 Common Failure Patterns

- ImagePullBackOff → wrong image or registry issue
- CrashLoopBackOff → app crashing repeatedly
- Pending → scheduling issue
- ContainerCreating stuck → volume problems

---

## 📝 Exam Tips

- events contain half the answers
- check namespace carefully
