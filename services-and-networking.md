# Services & Networking

## 🎯 Exam Objectives

- cluster networking basics
- services and service types
- CoreDNS
- network policies
- ingress

---

## 🛰 Service Types

| Type | Purpose |
|------|--------|
| ClusterIP | internal access |
| NodePort | exposes via node port |
| LoadBalancer | cloud LB integration |
| ExternalName | DNS aliasing |

### Create service
```
kubectl expose deployment web --port=80 --type=NodePort
```

---

## 🧭 Network Policies

Restrict traffic between pods.

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-frontend
spec:
  podSelector:
    matchLabels:
      role: frontend
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: backend
```

---

## 🌐 Ingress Example

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: web-ingress
spec:
  rules:
  - host: myapp.local
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: web
            port:
              number: 80
```

---

## 📝 Exam Tips

- verify ingress controller is installed
- NodePort range default: **30000–32767**
