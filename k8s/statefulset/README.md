
<a href="https://youtu.be/zj6r_EEhv6s" title="k8s-sts"><img src="https://i.ytimg.com/vi/zj6r_EEhv6s/hqdefault.jpg" width="20%" alt="k8s-sts" /></a> 


参考：https://www.youtube.com/watch?v=zj6r_EEhv6s

# Create a namespace

```
kubectl create ns example
```

# Check the storageclass for host path provisioner

```
kubectl get storageclass
```

# Deploy our statefulset

```
kubectl -n example apply -f .\kubernetes\statefulsets\statefulset.yaml
kubectl -n example apply -f .\kubernetes\statefulsets\example-app.yaml
```

# Enable Redis Cluster

```
$IPs = $(kubectl -n example get pods -l app=redis-cluster -o jsonpath='{range.items[*]}{.status.podIP}:6379 ')
kubectl -n example exec -it redis-cluster-0  -- /bin/sh -c "redis-cli -h 127.0.0.1 -p 6379 --cluster create ${IPs}"
kubectl -n example exec -it redis-cluster-0  -- /bin/sh -c "redis-cli -h 127.0.0.1 -p 6379 cluster info"
```

# More info

https://rancher.com/blog/2019/deploying-redis-cluster
