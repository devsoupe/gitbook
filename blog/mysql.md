---
description: 도커 환경에서 MySQL 설치 및 접속을 정리한 내용입니다.
---

# 도커 환경에서 MySQL 설치 및 접속

**macOS 기준으로 도커 환경에서 MySQL 설치 및 접속에 대한 가이드를 제공한다.**

## 1. 도커 설치

{% tabs %}
{% tab title="홈페이지에서 직접 설치" %}
### 다운로드 및 설치

* [도커 홈페이지](https://www.docker.com/products/docker-desktop/)에서 자신의 OS에 맞는 파일을 내려 받은 후 설치한다.

### 버전 확인

* 설치가 완료되면 버전을 출력해 정상적으로 출력되는지 확인한다.

```bash
$ docker -v 
Docker version 24.0.2, build cb74dfc
```
{% endtab %}

{% tab title="Homebrew Cask를 이용한 설치" %}
### 다운로드 및 설치

#### 1. Homebrew

* macOS에서 사용되는 인기있는 패키지 매니저이다.
* CLI를 통해 손쉽게 소프트웨어 패키지와 의존성을 설치, 업데이트 및 관리할 수 있다.
* [Homebrew 홈페이지](https://brew.sh/index\_ko)에 나와있는 명령어로 Homebrew를 설치한다.

```bash
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

#### 2. Homebrew Cask

* Homebrew의 확장으로 명령줄을 통해 그래픽 애플리케이션(예: GUI 앱)을 설치할 수 있다.
* 이를 설치하기 위해서는 먼저 Homebrew가 설치되어 있어야 한다.

```bash
$ brew install cask
```

#### 3. 도커

* 설치한 Homebrea Cask를 사용해 도커를 설치한다.

```bash
$ brew install --cask docker
```

### 버전 확인

* 설치가 완료되면 버전을 출력해 정상적으로 출력되는지 확인한다.

```bash
$ docker -v 
Docker version 24.0.2, build cb74dfc
```
{% endtab %}
{% endtabs %}

## 2. MySQL 이미지 다운로드

{% tabs %}
{% tab title="최신 버전 설치" %}
* `docker pull` 명령어를 사용해 MySQL 도커 이미지를 다운로드 한다.
* 태그에 버전을 명시하지 않으면 자동으로 최신 버전을 다운로드 한다.

```bash
$ docker pull mysql
Using default tag: latest
latest: Pulling from library/mysql
1817bc1e6309: Pull complete 
740bd54462bc: Pull complete 
a7e5ed4e69b3: Pull complete 
8fdf88d7bbb7: Pull complete 
a1a5f8560950: Pull complete 
82b514ba21a5: Pull complete 
d6a4cb36f5f9: Pull complete 
3392803e2ec5: Pull complete 
dcc1a15c36b9: Pull complete 
3e1c4ca2fc97: Pull complete 
Digest: sha256:6a5dbd2819e36048669639811461f27fee48da1e22039e5d31f4273a20d542f6
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest
```
{% endtab %}

{% tab title="버전 지정 설치" %}
* 특정한 MySQL 도커 이미지를 다운로드 받으려면 태그에 버전을 지정하면 된다.
* 사용 가능한 버전은 [dockerhub](https://hub.docker.com/\_/mysql/?tab=tags)에서 확인할 수 있다.
* 8.0.34 버전을 다운로드 하려면 다음과 같이 태그에 버전을 지정하면 된다.

```bash
$ docker pull mysql:8.0.34
8.0.34: Pulling from library/mysql
1817bc1e6309: Already exists 
740bd54462bc: Already exists 
a7e5ed4e69b3: Already exists 
8fdf88d7bbb7: Already exists 
a1a5f8560950: Already exists 
6d2014e71aa1: Pull complete 
a65eef362898: Pull complete 
1086465c0f61: Pull complete 
6d718a732c3a: Pull complete 
c724fd4b412f: Pull complete 
74fcbdd515b3: Pull complete 
Digest: sha256:51c4dc55d3abf4517a5a652794d1f0adb2f2ed1d1bedc847d6132d91cdb2ebbf
Status: Downloaded newer image for mysql:8.0.34
docker.io/library/mysql:8.0.34
```
{% endtab %}
{% endtabs %}

* `docker images` 명령어를 사용해 설치되어 있는 최신 버전과 지정한 8.0.34 버전을 확인할 수 있다.

```bash
$ docker images
REPOSITORY             TAG       IMAGE ID       CREATED       SIZE
mysql                  latest    de7c37d1d5ac   3 days ago    599MB
mysql                  8.0.34    2031a058d3ba   12 days ago   599MB
```

## 3. MySQL 도커 이미지로 컨테이너 생성 및 실행

* `docker run` 명령어를 사용해 다운로드 받은 이미지로 컨테이너를 실행할 수 있다.
* 생성 및 실행되는 컨테이너 이름은 mysql-container이다.
* MySQL 접속시 사용되는 루트 패스워드는 \<password>에 지정해주면 된다.

```bash
$ docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=<password> -d -p 3306:3306 mysql:latest
```

## 4. 실행중인 도커 컨테이너 리스트 출력

* `docker ps -a` 명령어로 컨테이너 생성 및 실행 후 정상적으로 실행되고 있는지 확인할 수 있다.

```bash
$ docker ps -a
CONTAINER ID   IMAGE                         COMMAND                  CREATED          STATUS          PORTS                               NAMES
70c1ef9b8e8c   772571a08c67                  "docker-entrypoint.s…"   56 minutes ago   Up 50 minutes   0.0.0.0:3306->3306/tcp, 33060/tcp   mysql-container

```

{% hint style="info" %}
실행중인 MySQL 도커 컨테이너 시작/중지/재시작 하려면 다음과 같은 명령어를 사용해야 한다.

\
`# MySQL 도커 컨테이너 중지`

`$ docker stop mysql-container`

\
`# MySQL Docker 컨테이너 시작`

`$ docker start mysql-container`\
\
`# MySQL 도커 컨테이너 재시작`

`$ docker restart mysql-container`
{% endhint %}

## 5. 실행중인 MySQL 도커 컨테이너 접속

* `docker exec` 명령어를 사용하여 도커 Docker 컨테이너를 정상적으로 실행했으면 컨테이너에 접속한다.
* 컨테이너에 접속해 MySQL 에도 접속하여 원하는 작업을 수행할 수 있다.

```bash
$ docker exec -it mysql-container bash
bash-4.4# mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 20
Server version: 8.0.33 MySQL Community Server - GPL

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| library            |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.01 sec)

mysql> 
```
