# setup

## 서버 준비

AWS 에서 t2.medium\(2 core 4 GiB\) 를 띄웠다.

## Docker 설치

```text
$ sudo yum update -y
$ sudo yum install docker -y
$ sudo service docker start
$ sudo usermod -a -G docker ec2-user
$ sudo systemctl enable docker.service
$ sudo systemctl start docker.service
```

## Kubernetes 설치

[https://twofootdog.tistory.com/8?category=845779](https://twofootdog.tistory.com/8?category=845779)

#### 사전 OS 설정

1. **SELinux설정을 permissive 모드로 변경**

   [https://www.redhat.com/ko/topics/linux/what-is-selinux](https://www.redhat.com/ko/topics/linux/what-is-selinux) SELinux\(Security-Enhanced Linux\)는 관리자가 시스템 액세스 권한을 효과적으로 제어할 수 있게 하는 Linux® 시스템용 보안 아키텍처 SELINUX=permissive를 설정하여 SELinux를 활성화

   ```text
   $ setenforce 0
   $ sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config
   $ sestatus
   ```

2. **br\_netfilter 활성화**

   [https://honggg0801.tistory.com/43](https://honggg0801.tistory.com/43) br\_netfilter 커널 모듈이 필요하다. 이 커널 모듈을 사용하면 브릿지를 통과하는 패킷이 필터링 및 포트 전달을 위해 iptables 에 의해 처리되고 클러스터의 쿠버네티스 Pod은 서로 통신 가능

   ```text
   $ lsmod | grep br_netfilter
   $ modprobe br_netfilter
   $ lsmod | grep br_netfilter
   br_netfilter           22256  0
   bridge                151336  1 br_netfilter
   ```

   **iptables 설정**

   브릿지 방화벽 작동

   0 : iptables 룰과 매칭시키지 않음 \(바이패스\)

   1 : 정상적인 방화벽 기능을 수행 \(iptables 매칭\)

   ```text
   $ sudo vim /etc/sysctl.d/k8s.conf
   net.bridge.bridge-nf-call-ip6tables = 1
   net.bridge.bridge-nf-call-iptables = 1
   $ sudo sysctl --system
   ```

3. **SWAP 메모리 비활성화**

   ```text
   $ sudo swapoff -a
   $ cat /etc/fstab
   ```

4. **서버 재기동**

   ```text
   $ sudo reboot
   ```

#### kubernetes 설치

1. **YUM 레파지토리 설정**

   ```text
   $ sudo vim /etc/yum.repos.d/kubernetes.repo
   [kubernetes]
   name=Kubernetes
   baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
   enabled=1
   gpgcheck=1
   repo_gpgcheck=1
   gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg <https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg>
   exclude=kube*
   ```

2. **kubeadm, kubectl, kubelet 설치**

   kops, minikube, kubespray등이 있다.

   ```text
   $ sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
   $ sudo systemctl enable kubelet
   $ sudo systemctl start kubelet
   ```

## 마스터\(Node\)서버 설정

앞서 작업한 인스턴스로 k8-base 이미지를 생성했다.

#### kubeadm 수행

```text
$ kubeadm init --pod-network-cidr=10.244.0.0/16 
```

이런 결과가 나온다.

```text
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  <https://kubernetes.io/docs/concepts/cluster-administration/addons/>

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 172.31.9.112:6443 --token 1trb9c.rt97xq4hddtf80rf \\
    --discovery-token-ca-cert-hash sha256:bb194c12b0b45507abb2d8bce1c53b647c715b68291c7d264cd464bdd70ecfe9
```

하라는 대로 했다.

```text
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

토큰 정보는 아래 명령어로 재 확인이 가능하다.

```text
$ kubeadm token list
```

해당 토큰은 24시간만 사용 가능하므로 24시간 이후에는 아래 명령어로 token을 새로 생성해서 join하면 된다.

```text
$ kubeadm token create
```

맨 마지막 parameter인 sha256값 확인은 아래 명령어를 실행하면 된다.

```text
# openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'
```

#### CNI 설치

CNI\(Container Network Interface\)

이 글에서는 CNI로 Flannel을 설치한다

```text
$ kubectl apply -f <https://raw.githubusercontent.com/coreos/flannel/2140ac876ef134e0ed5af15c65e414cf26827915/Documentation/kube-flannel.yml>
```

설치 전

```text
$ kubectl get pod --all-namespaces
NAMESPACE     NAME                                                                      READY   STATUS    RESTARTS   AGE
kube-system   coredns-66bff467f8-shgzg                                                  0/1     Pending   0          25m
kube-system   coredns-66bff467f8-wwdp6                                                  0/1     Pending   0          25m
kube-system   etcd-ip-172-31-9-112.ap-northeast-2.compute.internal                      1/1     Running   0          25m
kube-system   kube-apiserver-ip-172-31-9-112.ap-northeast-2.compute.internal            1/1     Running   0          25m
kube-system   kube-controller-manager-ip-172-31-9-112.ap-northeast-2.compute.internal   1/1     Running   0          25m
kube-system   kube-proxy-bcwcn                                                          1/1     Running   0          25m
kube-system   kube-scheduler-ip-172-31-9-112.ap-northeast-2.compute.internal            1/1     Running   0          25m
```

설치 후

```text
$ kubectl get pod --all-namespaces
NAMESPACE     NAME                                                                      READY   STATUS    RESTARTS   AGE
kube-system   coredns-66bff467f8-shgzg                                                  1/1     Running   0          29m
kube-system   coredns-66bff467f8-wwdp6                                                  1/1     Running   0          29m
kube-system   etcd-ip-172-31-9-112.ap-northeast-2.compute.internal                      1/1     Running   0          29m
kube-system   kube-apiserver-ip-172-31-9-112.ap-northeast-2.compute.internal            1/1     Running   0          29m
kube-system   kube-controller-manager-ip-172-31-9-112.ap-northeast-2.compute.internal   1/1     Running   0          29m
kube-system   kube-flannel-ds-amd64-8hls8                                               1/1     Running   0          70s
kube-system   kube-proxy-bcwcn                                                          1/1     Running   0          29m
kube-system   kube-scheduler-ip-172-31-9-112.ap-northeast-2.compute.internal            1/1     Running   0          29m
```

## **노드\(Node\)서버 설정**

### kubeadm join 실행

```text
$ sudo kubeadm join 172.31.9.112:6443 --token 1trb9c.rt97xq4hddtf80rf \\
    --discovery-token-ca-cert-hash sha256:bb194c12b0b45507abb2d8bce1c53b647c715b68291c7d264cd464bdd70ecfe9
```

행되어서 `--v2` 옵션을 붙여줬다.

```text
Failed to request cluster-info, will try again: Get <https://172.31.9.112:6443/api/v1/namespaces/kube-public/configmaps/cluster-info?timeout=10s:> net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers)
```

vpc 안에서 모든 inbound를 허용했다.

```text
This node has joined the cluster:
* Certificate signing request was sent to apiserver and a response was received.
* The Kubelet was informed of the new secure connection details.

Run 'kubectl get nodes' on the control-plane to see this node join the cluster.
```

#### **kubectl 허용**

노드서버에서 kubectl을 허용하려면 해준다. 마스터서버의 **$HOME/.kube/config**파일을 노드서버의 **$HOME/.kube/config**파일로 옮겨주면 된다.

```text
$ mkdir -p $HOME/.kube
$ vim $HOME/.kube/config
```

#### **노드 실행 확인**

```text
$ kubectl get nodes
$ kubectl get pod --all-namespaces -o wide
```

## **파드\(pod\) 배포하기**

마스터서버에서 간단한 pod를 배포해보자. test.yaml 파일을 만들고 아래 코드를 기입해보자.

```text
apiVersion: v1
kind: Pod
metadata:
  name: test-pod
  labels:
    app: testapp
spec:
  containers:
  - name: test-container
    image: busybox
    command: ['sh', '-c', 'echo test && sleep 360']
```

그리고 아래 명령어로 해당 pod를 배포해보자.

```text
$ kubectl apply -f test.yaml
```

그리고 배포된 결과를 확인해보자.

```text
$ kubectl get pod --all-namespaces -o wide
```

. 아래 명령어를 통해 해당 pod의 로그를 확인할 수 있다.

```text
$ kubectl logs test-pod
```

warning 두가지가 거슬리지만 수정하지 않았다.

1. \[WARNING IsDockerSystemdCheck\]: detected "cgroupfs" as the Docker cgroup driver. The recommended driver is "systemd". Please follow the guide at [https://kubernetes.io/docs/setup/cri/](https://kubernetes.io/docs/setup/cri/)
2. \[WARNING FileExisting-tc\]: tc not found in system path

