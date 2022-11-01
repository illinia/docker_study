### 8.1 헬스 체크를 지원하는 도커 이미지 빌드하기

``docker container run -d -p 8080:80 diamol/ch08-numbers-api``

4번 실행
``curl http://localhost:8080/rng``

``docker container ls``

``docker image build -t diamol/ch08-numbers-api:v2 -f ./numbers-api/Dockerfile.v2 .``

``docker container run -d -p 8081:80 diamol/ch08-numbers-api:v2``

30 초 정도 기다리고
``docker container ls``

4번 실행
``curl http://localhost:8081/rng``

``docker container ls``

``docker container inspect 컨테이너``

### 8.2 디펜던시 체크가 적용된 컨테이너 실행하기

``docker container rm -f $(docker container ls -aq)``

``docker container run -d -p 8082:80 diamol/ch08-numbers-web``

``docker container ls``

``docker container run -d -p 8084:80 diamol/ch08-numbers-web:v2``

``docker container ls --all``

### 8.3 애플리케이션 체크를 위한 커스텀 유틸리티 만들기

``docker container rm -f $(docker container ls -aq)``

``docker container run -d -p 8080:80 --health-interval 5s diamol/ch08-numbers-api:v3``

5초 정도 기다린 후
``docker container ls``

4번 호출
``curl http://localhost:8080/rng``

http 테스트 유틸리티가 잘 작동한다
``docker container ls``

``docker container run -d -p 8081:80 diamol/ch08-numbers-web:v3``

``docker container ls --all``

### 8.4 도커 컴포즈에 헬스 체크와 디펜던시 체크 정의하기

컴포즈 파일이 있는 디렉터리 이동
``docker container rm -f $(docker container ls -aq)``

``docker-compose up -d``

5초 기다린 후
``docker container ls``

``docker container logs numbers-web컨테이너``

