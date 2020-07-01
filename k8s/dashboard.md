# dashboard

## Kubernetes Dashboard 설치

```text
kubectl apply -f <https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta1/aio/deploy/recommended.yaml>
```

### kubectl proxy 로 접근

```text
$ kubectl proxy --port=8001 &
[1] 27675
[ec2-user@ip-172-31-9-112 ~]$ Starting to serve on 127.0.0.1:8001
```

해제 방법

```text
netstat -tulp | grep kubectl
sudo kill -9 <pid>
```

putty로 proxy tunnel 만들어서 접근해야한다.

![](../.gitbook/assets/image%20%2850%29.png)

[http://127.0.0.1:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/\#/login](http://127.0.0.1:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login)

### 로그인 인증키 생성

서비스 어카운트 생성

```text
$ cat <<EOF | kubectl create -f -
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kube-system
EOF
serviceaccount/admin-user created
```

ClusterRoleBinding 생성

```text
$ cat <<EOF | kubectl create -f -
 apiVersion: rbac.authorization.k8s.io/v1
 kind: ClusterRoleBinding
 metadata:
   name: admin-user
 roleRef:
   apiGroup: rbac.authorization.k8s.io
   kind: ClusterRole
   name: cluster-admin
 subjects:
 - kind: ServiceAccount
   name: admin-user
   namespace: kube-system
EOF
clusterrolebinding.rbac.authorization.k8s.io/admin-user created
```

생성된 사용자 계정의 토큰

```text
$ kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')
Name:         admin-user-token-5v8rq
Namespace:    kube-system
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: admin-user
              kubernetes.io/service-account.uid: 88aef4df-b5e7-4aef-b6d7-445945468233

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1025 bytes
namespace:  11 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6IlVXMlBnS1pfRnBFRzh3UFBjbEp3UzFtMDNtaDROMmdGdVdIYnFOWkQ1MlEifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLTV2OHJxIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiI4OGFlZjRkZi1iNWU3LTRhZWYtYjZkNy00NDU5NDU0NjgyMzMiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZS1zeXN0ZW06YWRtaW4tdXNlciJ9.CpCLdd2jC9fI9ew3FqESbGCCKY_1hlP6BqD1VJa0w4dAH6mHuHCkCM5i3bHkZ0IGcqIQHmhVLLgqGM8xBlv7AY5vnniyU6EFGv9pPc6JiJsEehRF4_xBGitCFyhgtZHLUzOlQVraLWzsbTzFq1lC1BKxVP13BjF7VvplL3f0UB1ZBbefGuYAZlsW6Y_zrNm7wTdVx8aJe0LzowgGMQy8BahdFVV8xPpK5G2qnFfbtMkUr_0LUgDE4n58eQ13wJ0YHv0U6BBdHZZ_iDQvkyySURNALslzmm0TkmegDaZ_SmHD_IFQg9FCQA1ozRhqxW1cGWx0zncVlpn7oPJnZMs0wQ
```

![](../.gitbook/assets/image%20%2851%29.png)

