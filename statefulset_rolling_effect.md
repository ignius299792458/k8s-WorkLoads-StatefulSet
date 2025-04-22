# Stateful Set Rolling effect
When statefulsets pod get deleted, crashed, anytime. The replicas get maintained automatically with all previous crashed/deleted data and state of pod, a new one with stateful information of pervious pod.

Example: let try first multiple deletes then check rolling effect (auto-healing) and new pod's state informations
```
➜  mysql git:(main) kubectl delete pod mysql-statefulset-0 -n mysql-ns
pod "mysql-statefulset-0" deleted

➜  mysql git:(main) kubectl get pods -n mysql-ns
NAME                  READY   STATUS    RESTARTS   AGE
mysql-statefulset-0   1/1     Running   0          8s
mysql-statefulset-1   1/1     Running   0          28m
mysql-statefulset-2   1/1     Running   0          27m

➜  mysql git:(main) kubectl delete pod mysql-statefulset-0 -n mysql-ns
pod "mysql-statefulset-0" deleted

➜  mysql git:(main) kubectl get pods -n mysql-ns                      
NAME                  READY   STATUS              RESTARTS   AGE
mysql-statefulset-0   0/1     ContainerCreating   0          2s
mysql-statefulset-1   1/1     Running             0          28m
mysql-statefulset-2   1/1     Running             0          27m

➜  mysql git:(main) kubectl delete pod mysql-statefulset-0 -n mysql-ns
pod "mysql-statefulset-0" deleted

➜  mysql git:(main) kubectl get pods -n mysql-ns                      
NAME                  READY   STATUS              RESTARTS   AGE
mysql-statefulset-0   0/1     ContainerCreating   0          1s
mysql-statefulset-1   1/1     Running             0          28m
mysql-statefulset-2   1/1     Running             0          27m

➜  mysql git:(main) kubectl get pods -n mysql-ns
NAME                  READY   STATUS    RESTARTS   AGE
mysql-statefulset-0   1/1     Running   0          6s
mysql-statefulset-1   1/1     Running   0          28m
mysql-statefulset-2   1/1     Running   0          27m


```
