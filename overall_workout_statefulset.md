# Illustration of overall Workout of statefulset flow

## namespace
First implementation of overall namespace isolation for mysql resouces
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

## service or service-proxy
```
➜  git:(main) kubectl apply -f service.yml 
service/mysql-service created

➜  git:(main) kubectl get services
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   2m19s

➜  git:(main) kubectl get services -n mysql-ns
NAME            TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)    AGE
mysql-service   ClusterIP   None         <none>        3306/TCP   15s

```
