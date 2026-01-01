# Storage

## 🎯 Exam Objectives

- persistent volumes
- persistent volume claims
- storage classes
- dynamic provisioning
- configmaps and secrets

---

## 📦 Persistent Volume Example

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv1
spec:
  capacity:
    storage: 2Gi
  accessModes:
  - ReadWriteOnce
  hostPath:
    path: /data/pv1
```

## 🧾 Persistent Volume Claim

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc1
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

---

## 🧰 Mount in Pod

```yaml
volumes:
- name: data
  persistentVolumeClaim:
    claimName: pvc1
```

---

## 📝 Exam Tips

- PVC must match storage class & access mode
