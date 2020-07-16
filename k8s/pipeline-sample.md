# pipeline sample

## 환경 설정

### docker 설치

```text
$ sudo yum install docker -y
$ sudo systemctl enable docker.service
$ sudo systemctl start docker.service
```

#### ubuntu

```text
$ curl -fsSL https://get.docker.com/ | sudo sh
$ sudo usermod -aG docker ubuntu
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
$ curl -X POST http://127.0.0.1/jobs --header "Content-Type: application/json" --data '{"username":"ebhwang", "a":"a", "b": "b"}'
```

```text
$ curl -X GET http://127.0.0.1/jobs/102 --header "Content-Type: application/json"
```

## Docker 빌드

```
$ sudo docker build -t python-application .
```

실행확

```text
$ sudo docker run --name db \
  -e POSTGRES_DB=pipeline-sample \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=postgres \
  -e POSTGRES_INITDB_ARGS=--encoding=UTF-8 \
  -p 5432:5432 \
  -d postgres

$ sudo docker run -dit --name myapp \
  -e DB_HOST=52.79.154.184 \
  -e DB_PORT=5432 \
  -e DB_NAME=pipeline-sample \
  -e DB_USERNAME=postgres \
  -e DB_PASSWORD=postgres \
  -p 8080:5000 python-application:0.0.1

```

접속확인

[http://52.79.154.184:8080/](http://52.79.154.184:8080/)

```text
$ psql -h localhost -p 5432 -U postgres
```

#### Docker Push

```text
$ docker tag python-application:latest ebhwang/python-application:latest
$ docker push ebhwang/python-application:latest
```

## k3s 설치

[https://si.mpli.st/dev/2020-01-01-easy-k8s-with-k3s/](https://si.mpli.st/dev/2020-01-01-easy-k8s-with-k3s/)

```text
$ curl -sfL https://get.k3s.io | sh -
```

### Pod 생성

#### Deployment 생성

```text

```

