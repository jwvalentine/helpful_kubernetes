# Helpful Kubernetes Commands for Daily Use

A quick reference for the `kubectl` commands you'll reach for most often. Organized by task so you can find what you need fast.

---

## 1. Pods

### List pods
```bash
kubectl get pods
kubectl get pods -A
kubectl get pods -n <namespace>
```

### Describe a pod
```bash
kubectl describe pod <pod-name>
```

### Get pod YAML
```bash
kubectl get pod <pod-name> -o yaml
```

### Delete a pod
```bash
kubectl delete pod <pod-name>
```

### Force delete a pod
```bash
kubectl delete pod <pod-name> --force --grace-period=0
```

---

## 2. Deployments

### List deployments
```bash
kubectl get deploy
kubectl get deploy -A
kubectl get deploy -n <namespace>
```

### Describe a deployment
```bash
kubectl describe deploy <deployment-name>
```

### Get deployment YAML
```bash
kubectl get deploy <deployment-name> -o yaml
```

### Create a deployment
```bash
kubectl create deployment <name> --image=<image>
```

### Scale a deployment
```bash
kubectl scale deploy <deployment-name> --replicas=5
```

### Rolling restart
```bash
kubectl rollout restart deploy <deployment-name>
```

### Rollout status
```bash
kubectl rollout status deploy <deployment-name>
```

### Rollout history
```bash
kubectl rollout history deploy <deployment-name>
```

### Rollback to previous version
```bash
kubectl rollout undo deploy <deployment-name>
```

---

## 3. Services

### List services
```bash
kubectl get svc
```

### Describe a service
```bash
kubectl describe svc <service-name>
```

### Expose a deployment
```bash
kubectl expose deploy <deployment-name> --port=80 --target-port=8080 --type=ClusterIP
```

### View endpoints
```bash
kubectl get endpoints <service-name>
```

---

## 4. Namespaces

### List namespaces
```bash
kubectl get ns
```

### Create a namespace
```bash
kubectl create ns <namespace>
```

### Delete a namespace
```bash
kubectl delete ns <namespace>
```

### Set default namespace for current context
```bash
kubectl config set-context --current --namespace=<namespace>
```

---

## 5. Nodes

### List nodes
```bash
kubectl get nodes
```

### Describe a node
```bash
kubectl describe node <node-name>
```

### Cordon / uncordon a node
```bash
kubectl cordon <node-name>
kubectl uncordon <node-name>
```

### Drain a node (for maintenance)
```bash
kubectl drain <node-name> --ignore-daemonsets --delete-emptydir-data
```

---

## 6. Config & Contexts

### List all contexts
```bash
kubectl config get-contexts
```

### Switch context
```bash
kubectl config use-context <context-name>
```

### Show current context
```bash
kubectl config current-context
```

### View full kubeconfig
```bash
kubectl config view
```

---

## 7. Logs

### Basic logs
```bash
kubectl logs <pod-name>
```

### Logs for a specific container
```bash
kubectl logs <pod-name> -c <container-name>
```

### Stream logs in real time
```bash
kubectl logs -f <pod-name>
```

### Logs from a previous (crashed) container
```bash
kubectl logs <pod-name> -c <container-name> --previous
```

---

## 8. Exec Into Containers

### Open a bash shell
```bash
kubectl exec -it <pod-name> -- bash
```

### Open a sh shell (for minimal images)
```bash
kubectl exec -it <pod-name> -- sh
```

### Exec into a specific container in a pod
```bash
kubectl exec -it <pod-name> -c <container-name> -- bash
```

---

## 9. Copying Files

### Copy from container to local
```bash
kubectl cp <namespace>/<pod-name>:<path> <local-path>
```

### Copy from local to container
```bash
kubectl cp <local-path> <namespace>/<pod-name>:<path>
```

---

## 10. Debugging

### Port forward to a pod
```bash
kubectl port-forward <pod-name> 8080:80
```

### Attach an ephemeral debug container
```bash
kubectl debug -it <pod-name> --image=busybox
```

### View recent cluster events
```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```

### Inspect environment variables
```bash
kubectl exec <pod-name> -- env
```

### Inspect the filesystem
```bash
kubectl exec <pod-name> -- ls -al /
```

### Explain a resource's fields
```bash
kubectl explain deploy
kubectl explain pod.spec.containers
```

---

## 11. Applying Manifests

### Apply a manifest (create or update)
```bash
kubectl apply -f <file.yaml>
kubectl apply -f <directory/>
```

### Replace a resource
```bash
kubectl replace -f <file.yaml>
```

### Delete resources defined in a manifest
```bash
kubectl delete -f <file.yaml>
```

### Dry run (preview changes without applying)
```bash
kubectl apply -f <file.yaml> --dry-run=client
```

---

## 12. Quick Resource Creation

### Generate a deployment manifest template
```bash
kubectl create deploy myapp --image=nginx --dry-run=client -o yaml > myapp.yaml
```

### Create a secret from a literal value
```bash
kubectl create secret generic my-secret --from-literal=password=1234
```

### Create a configmap from a file
```bash
kubectl create configmap my-config --from-file=config.json
```

---

## 13. CronJobs & Jobs

### List CronJobs
```bash
kubectl get cronjob
```

### Trigger a CronJob manually
```bash
kubectl create job --from=cronjob/<cron-name> manual-run
```

### Describe a job
```bash
kubectl describe job <job-name>
```

---

## 14. Useful Aliases

Save these in your shell profile (`~/.bashrc`, `~/.zshrc`, etc.) to speed up your workflow.

```bash
alias k=kubectl
alias kgp='kubectl get pods'
alias kgs='kubectl get svc'
alias kgd='kubectl get deploy'
alias kctx='kubectl config use-context'
alias kn='kubectl config set-context --current --namespace'
```

---

## Support

If this has helped you in some meaningful way, please consider buying me a coffee: https://buymeacoffee.com/jwvalentine
