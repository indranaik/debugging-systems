# Kubernetes Debugging Commands

## Cluster Health

```bash
kubectl get nodes
kubectl top nodes
kubectl top pods -A
```

## Pod Analysis

```bash
kubectl describe pod <pod>
kubectl logs <pod>
kubectl exec -it <pod> -- sh
```

## Events

```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```

## Networking

```bash
kubectl get svc
kubectl get endpoints
kubectl get networkpolicy
```

## Node Debugging

```bash
kubectl describe node <node>
kubectl cordon <node>
kubectl drain <node>
```

## Resource Analysis

```bash
kubectl top pods
kubectl describe pod
```

## Restart Detection

```bash
kubectl get pods
kubectl describe pod
```
