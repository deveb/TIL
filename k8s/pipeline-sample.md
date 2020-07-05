# pipeline sample

## 개발환경

### docker 설치

```text
$ sudo yum install docker -y
$ sudo systemctl enable docker.service
$ sudo systemctl start docker.service
```

### docker-compose 설치

{% embed url="https://docs.docker.com/compose/install/\#install-compose-on-linux-systems" %}

```text
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.26.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
$ docker-compose --version
docker-compose version 1.26.1, build f216ddbf
```

### git 설치

```text
$ sudo yum update -y
$ sudo yum install git -y
```

### git repository 클론

```text
$ git clone https://github.com/deveb/ML-Study.git
$ cd MLOps/pipeline-sample/
```

### 실행

```text
$ sudo docker-compose up -d
```

## 테스

```text
curl -X POST http://52.79.177.238/jobs --header "Content-Type: application/json" --data '{"username":"ebhwang", "a":"a", "b": "b"}'
```

```text
curl -X GET http://52.79.177.238/jobs/102 --header "Content-Type: application/json"
```



