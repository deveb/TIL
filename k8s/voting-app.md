# voting app

Running in a GKE environment

{% embed url="https://github.com/mmumshad/kubernetes-example-voting-app" %}

```bash
git clone https://github.com/mmumshad/kubernetes-example-voting-app.git
cd kubernetes-example-voting-app/
kubectl create -f ./
```

```text
$ kubectl get services
NAME             TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)        AGE
db               ClusterIP      10.104.15.217   <none>         5432/TCP       2m35s
kubernetes       ClusterIP      10.104.0.1      <none>         443/TCP        40m
redis            ClusterIP      10.104.11.213   <none>         6379/TCP       2m34s
result-service   LoadBalancer   10.104.15.114   34.85.1.67     80:30156/TCP   2m34s
voting-service   LoadBalancer   10.104.10.203   34.85.83.229   80:31506/TCP   2m34s
```

![](../.gitbook/assets/image%20%2852%29.png)



