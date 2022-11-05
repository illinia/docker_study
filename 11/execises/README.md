### 11.2 도커를 이용한 빌드 인프라스트럭처 구축하기

``docker-compose -f docker-compose.yml -f docker-compose-linux.yml up -d``

``echo $'\n127.0.0.1 registry.local' | sudo tee -a /etc/hosts``

### 11.3 도커 컴포즈를 이용한 빌드 설정

``docker-compose -f docker-compose.yml -f docker-compose-build.yml build``

``docker image inspect -f '{{.Config.Labels}}' diamol/ch11-numbers-api:v3-build-local``

``docker image build -f numbers-api/Dockerfile.v4 --build-arg BUILD_TAG=ch11 -t numbers-api .``

``docker image inspect -f '{{.Config.Labels}}' numbers-api``

### 11.4 도커 외의 의존 모듈이 불필요한 CI 작업 만들기

``docker-compose -f docker-compose.yml -f docker-compose-build.yml build``

``docker image inspect -f '{{.config.Labels}}' diamol/ch11-numbers-api:v3-build-local``

``docker image build -f numbers-api/Dockerfile.v4 --build-arg BUILD_TAG=ch11 -t numbers-api .``

``docker image inspect -f '{{.Config.Labels}}' numbers-api``

