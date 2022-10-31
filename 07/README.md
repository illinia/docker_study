### 7.1 도커 컴포즈 파일의 구조

``docker network create nat``

``docker-compose up``

### 7.2 도커 컴포즈를 사용해 여러 컨테이너로 구성된 애플리케이션 실행하기

image-of-the-day 디렉토리 이동
``docker-compose up --detach``

``docker-compose up -d --scale iotd=3``

``docker-compose logs --tail=1 iotd``

``docker-compose stop``

``docker-compose start``

``docker container ls``

### 7.3 도커 컨테이너 간의 통신

``docker-compose up -d --scale iotd=3``

``docker container exec -it 컨테이너이름 sh``

``nslookup accesslog``

``docker container rm -f accesslog_컨테이너이름``

``docker-compose up -d --scale iotd=3``

``docker container exec -it 컨테이너이름 sh``

``nslookup accesslog``

``nslookup iotd``

### 7.4 도커 컴포즈로 애플리케이션 설정값 지정하기

``docker-compose up -d``

``docker-compose ps``

### lab

``docker-compose -f docker-compose-dev.yml up -d``

``docker-compose -f docker-compose-test.yml up -d``