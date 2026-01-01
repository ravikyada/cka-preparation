# Workloads & Scheduling

## 🎯 Exam Objectives

- create and manage workloads
- deployments, replicasets, pods
- statefulsets and daemonsets
- scheduling pods to nodes
- labels, selectors, affinities
- jobs and cronjobs

---

## 📦 Creating Workloads

### Pod
```
kubectl run nginx --image=nginx
```

### Deployment
```
kubectl create deployment web --image=nginx --replicas=3
```

### DaemonSet
DaemonSets run one pod per node.

Example YAML:
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: node-exporter
spec:
  selector:
    matchLabels:
      app: node-exporter
  template:
    metadata:
      labels:
        app: node-exporter
    spec:
      containers:
      - name: node-exporter
        image: prom/node-exporter
```

### StatefulSet (stable network identity)
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: db
spec:
  serviceName: db
  replicas: 3
  selector:
    matchLabels:
      app: db
  template:
    metadata:
      labels:
        app: db
    spec:
      containers:
      - name: db
        image: redis
```

---

## ⏱ Scheduling Control

### Taints & Tolerations
```yaml
tolerations:
- key: "dedicated"
  operator: "Equal"
  value: "db"
  effect: "NoSchedule"
```

### Node Affinity
```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: role
          operator: In
          values:
          - backend
```

---

## 🐞 Troubleshooting Scheduling

- pod pending = check events
```
kubectl describe pod podname
```

Possible causes:

- taints
- resource requests too high
- missing node selector match

---

## 📝 Exam Tips

- use `kubectl create deployment -o yaml --dry-run=client`
- remember: StatefulSets require headless service
