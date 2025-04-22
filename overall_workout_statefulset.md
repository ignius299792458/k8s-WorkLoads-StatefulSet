# Illustration of overall Workout of statefulset flow

## namespace
```
➜ git:(main) kubectl apply -f namespace.yml 
namespace/mysql-ns created

➜ git:(main) kubectl get namespaces
NAME                 STATUS   AGE
default              Active   7d3h
kube-node-lease      Active   7d3h
kube-public          Active   7d3h
kube-system          Active   7d3h
local-path-storage   Active   7d3h
`mysql-ns             Active   7s`

```
