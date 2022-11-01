### 9.1 컨테이너화된 애플리케이션에서 사용되는 모니터링 기술 스택

도커 엔진 daemon 설정
"metrics-addr": "127.0.0.1:9323"
"experimental": true

로컬 컴퓨터 IP 주소를 확인해 환경 변수로 정의하기
``hostIP=$(ifconfig en0 | grep -e 'inet\s' | awk '{print $2}')``

``docker container run -e DOCKER_HOST=$hostIP -d -p 9090:9090 diamol/prometheus:2.13.1``

### 9.2 애플리케이션의 측정값 출력하기

``docker container rm -f $(docker container ls -aq)``

``docker network create nat``

``docker-compose up -d``

http://localhost:8010/metrics 에서 측정값을 볼 수 있다.

``for i in {1..5}; do curl http://localhost:8010 > /dev/null; done``

### 9.3 측정값 수집을 맡을 프로메테우스 컨테이너 실행하기

``docker-compose -f docker-compose-scale.yml up -d --scale accesslog=3``

``for i in {1..10}; do curl http://localhost:8010 > /dev/null; done``

### 9.4 측정값 시각화를 위한 그라파나 컨테이너 실행하기

``export HOST_IP=$(ifconfig en0 | grep -e 'inet\s' | awk '{print $2}')``

``docker-compose -f ./docker-compose-with-grafana.yml up -d --scale accesslog=3``

``for i in {1..20}; do curl http://localhost:8010 > /dev/null; done``

