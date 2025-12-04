# Quick-List of Helpful Kubernetes Commands for Daily Use

## 1. Managing Pods

### List pods
```
kubectl get pods
kubectl get pods -A
kubectl get pods -n <namespace>
```

### Describe a pod
```
kubectl describe pod <pod-name>
```

### Get pod YAML
```
kubectl get pod <pod-name> -o yaml
```

### Delete pod
```
kubectl delete pod <pod-name>
```

### Force delete
```
kubectl delete pod <pod-name> --force --grace-period=0
```

## 2. Managing Nodes

### List nodes
```
kubectl get nodes
```

### Node details
```
kubectl describe node <node-name>
```

### Cordon / Uncordon
```
kubectl cordon <node-name>
kubectl uncordon <node-name>
```

### Drain node
```
kubectl drain <node-name> --ignore-daemonsets --delete-emptydir-data
```

## 3. Logging From Pods

### Basic logs
```
kubectl logs <pod-name>
```

### Specific container logs
```
kubectl logs <pod-name> -c <container-name>
```

### Follow logs
```
kubectl logs -f <pod-name>
```

### Previous crashed container logs
```
kubectl logs <pod-name> -c <container-name> --previous
```

## 4. Exec Into Containers

### Bash shell
```
kubectl exec -it <pod-name> -- bash
```

### sh shell
```
kubectl exec -it <pod-name> -- sh
```

### Exec into specific container
```
kubectl exec -it <pod-name> -c <container-name> -- bash
```

## 5. Copy Files

### Container → local
```
kubectl cp <namespace>/<pod-name>:<path> <local-path>
```

### Local → container
```
kubectl cp <local-path> <namespace>/<pod-name>:<path>
```

## 6. Debugging Helpers

### Port forward
```
kubectl port-forward <pod-name> 8080:80
```

### Ephemeral debug container
```
kubectl debug -it <pod-name> --image=busybox
```

## 7. Managing Deployments

### List deployments
```
kubectl get deploy
kubectl get deploy -A
kubectl get deploy -n <namespace>
```

### Describe deployment
```
kubectl describe deploy <deployment-name>
```

### Deployment YAML
```
kubectl get deploy <deployment-name> -o yaml
```

### Create deployment
```
kubectl create deployment <name> --image=<image>
```

### Scale deployment
```
kubectl scale deploy <deployment-name> --replicas=5
```

### Rollout restart
```
kubectl rollout restart deploy <deployment-name>
```

### Rollout status
```
kubectl rollout status deploy <deployment-name>
```

### Rollback
```
kubectl rollout undo deploy <deployment-name>
```

### Rollout history
```
kubectl rollout history deploy <deployment-name>
```

## 8. Apply / Update Manifests

### Apply
```
kubectl apply -f <file.yaml>
kubectl apply -f <directory/>
```

### Replace
```
kubectl replace -f <file.yaml>
```

### Delete via file
```
kubectl delete -f <file.yaml>
```

### Dry run
```
kubectl apply -f <file.yaml> --dry-run=client
```

## 9. Services

### List services
```
kubectl get svc
```

### Describe service
```
kubectl describe svc <service-name>
```

### Expose deployment
```
kubectl expose deploy <deployment-name> --port=80 --target-port=8080 --type=ClusterIP
```

### Endpoints
```
kubectl get endpoints <service-name>
```

## 10. Namespaces

### List namespaces
```
kubectl get ns
```

### Create namespace
```
kubectl create ns <namespace>
```

### Delete namespace
```
kubectl delete ns <namespace>
```

### Set default namespace
```
kubectl config set-context --current --namespace=<namespace>
```

## 11. Config & Context

### List contexts
```
kubectl config get-contexts
```

### Switch context
```
kubectl config use-context <context-name>
```

### Current context
```
kubectl config current-context
```

### View config
```
kubectl config view
```

## 12. Aliases

```
alias k=kubectl
alias kgp='kubectl get pods'
alias kgs='kubectl get svc'
alias kgd='kubectl get deploy'
alias kctx='kubectl config use-context'
alias kn='kubectl config set-context --current --namespace'
```

## 13. Resource Debugging

### Events
```
kubectl get events --sort-by=.metadata.creationTimestamp
```

### Env vars
```
kubectl exec <pod> -- env
```

### File system
```
kubectl exec <pod> -- ls -al /
```

### Explain resource
```
kubectl explain deploy
kubectl explain pod.spec.containers
```

## 14. Quick Resource Creation

### Generate manifest template
```
kubectl create deploy myapp --image=nginx --dry-run=client -o yaml > myapp.yaml
```

### Create secret
```
kubectl create secret generic my-secret --from-literal=password=1234
```

### Create configmap
```
kubectl create configmap my-config --from-file=config.json
```

## 15. CronJobs and Jobs

### List CronJobs
```
kubectl get cronjob
```

### Run CronJob manually
```
kubectl create job --from=cronjob/<cron-name> manual-run
```

### Describe job
```
kubectl describe job <job-name>
```
