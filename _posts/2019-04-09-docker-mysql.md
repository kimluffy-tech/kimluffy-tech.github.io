---
layout: post
title:  "Windows 에서 Docker 로 MYSQL 사용하기"
categories: docker
---
## 목표

- Windows 에서 Docker 로 MYSQL 을 사용해보자.

## 시작하며

- 처음 개인 프로젝트를 생성했을 땐 MYSQL을 로컬에 설치하였고,  
AWS를 알게 된 후에는 AWS의 RDS를 이용. 편리함을 느꼈지만 편리한만큼 지출이 생겼다.  
이제 Doker를 통해 조금 더 쉽고, 편리하게 ~~지출없이~~ 로컬 개발환경을 꾸려보자.

---

1. MYSQL 이미지 다운로드
- MYSQL 이미지 다운로드
```
docker pull mysql:5.7
```
- 이미지 목록 확인
```
docker images
```
2. MYSQL 컨테이너 설치 및 실행
- MYSQL 컨테이너 설치 및 실행
```
docker run -d -p 33061:3306 -e MYSQL_ROOT_PASSWORD=password --name springsbootwebstudy-mysql mysql:5.7
```
- 컨테이너 전체 목록 확인
```
docker ps -a
```
3. 그 외 명령어
- MYSQL 컨테이너 bash 접속
```
docker exec -it springsbootwebstudy-mysql bash
```
- MYSQL 서버 접속
```
mysql -u root -p
```
- 컨테이너 정지
```
docker stop springsbootwebstudy-mysql
```
- 컨테이너 시작
```
docker start springsbootwebstudy-mysql
```
- 컨테이너 삭제
```
docker rm springsbootwebstudy-mysql
```
- 이미지 삭제
```
docker rmi mysql:5.7
```
4. workbench 접속 정보
- Hostname : localhost
- Port : 33061
- Username : root
- Password : password
* Windows 7 에서 Hostname 을 localhost 로 하여 접속이 되지 않을 경우  
**192.168.99.100** 으로 변경 후 재시도 해보세요.
