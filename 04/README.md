### 4.1 Dockerfile 이 있는데 빌드 서버가 필요할까?
``docker image build -t multi-stage .``

### 4.2 애플리케이션 빌드 실전 예제: 자바 소스 코드
``docker image build -t image-of-the-day .``

``docker network create nat``

``docker container run --name iotd -d -p 800:80 --network nat image-of-the-day``

### 4.3 애플리케이션 빌드 실전 예제: Node.js 소스 코드
``docker image build -t access-log .``

``docker container run --name accesslog -d -p 801:80 --network nat access-log``

### 4.4 애플리케이션 빌드 실전 예제: Go 소스 코드
``docker image build -t image-gallery .``

``docker container run -d -p 802:80 --network nat image-gallery``