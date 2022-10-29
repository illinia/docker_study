### 3.1 도커 허브에 공유된 이미지 사용하기
``docker image pull diamol/ch03-web-ping``

* -d 는 --detach 축약형
* --name 컨테이너에 원하는 이름 붙이고 지칭할 수 있음

``docker container run -d --name web-ping diamol/ch03-web-ping``

``docker rm -f web-ping``

``docker container run --env TARGET=google.com diamol/ch03-web-ping``

### 3.3 컨테이너 이미지 빌드하기
``docker image build --tag web-ping .``

``docker image ls 'w*'``

``docker container run -e TARGET=docker.com -e INTERVAL=5000 web-ping``

### 3.4 도커 이미지와 이미지 레이어 이해하기
``docker image history web-ping``

``docker image ls``

``docker system df``

### 3.5 이미지 레이어 캐시를 이용한 Dockerfile 스크립트 최적화
``docker image build -t web-ping:v2 .``

### 연습문제

``docker container run -it --name ch03lab diamol/ch03-lab``
``echo test >> ch03.txt``
``exit``
``docker container commit ch03lab ch03-lab-soln``
``docker container run ch03-lab-soln cat ch03.txt``