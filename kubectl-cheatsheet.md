# Kubectl Cheat Sheet

## Contexts

```
kubectl config get-contexts
kubectl config use-context <name>
```

## Generators

```
kubectl run nginx --image=nginx
kubectl create deploy web --image=nginx
```

## YAML from command

```
kubectl create deploy web --image=nginx -o yaml --dry-run=client
```

## Editing resources

```
kubectl edit deploy web
```

## Labels & Selectors

```
kubectl get pods -l app=web
```

## Debugging

```
kubectl describe pod
kubectl logs pod
```
