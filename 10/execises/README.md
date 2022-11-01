### 10.1 도커 컴포즈로 여러개의 애플리케이션 배포하기

``docker-compose -f ./numbers/docker-compose.yml up -d``

``docker-compose -f ./todo-list/docker-compose.yml up -d``

``docker-compose -f ./todo-list/docker-compose.yml up -d``

``docker-compose -f ./todo-list/docker-compose.yml -p todo-test up -d``

``docker container port todo-test-todo-web-1 80``

### 10.2 도커 컴포즈의 오버라이드 파일

``docker-compose -f ./todo-list/docker-compose.yml -f ./todo-list/docker-compose-v2.yml config``

``docker container rm -f $(docker container ls -aq)``

``docker-compose -f ./numbers/docker-compose.yml -f ./numbers/docker-compose-dev.yml -p numbers-dev up -d``

``docker-compose -f ./numbers/docker-compose.yml -f ./numbers/docker-compose-test.yml -p numbers-test up -d``

``docker-compose -f ./numbers/docker-compose.yml -f ./numbers/docker-compose-uat.yml -p numbers-uat up -d``

``docker-compose down``

``docker-compose -f ./numbers/docker-compose.yml -f ./numbers/docker-compose-test.yml down``

``docker-compose -f ./numbers/docker-compose.yml -f ./numbers/docker-compose-test.yml -p numbers-test down``

### 10.3 환경 변수와 비밀값을 이용해 설정 주입하기

``docker container rm -f $(docker container ls -aq)``

``docker-compose -f ./todo-list-configured/docker-compose.yml -f ./todolist-configured/docker-compose-dev.yml -p todo-dev up -d``

``curl http://localhost:8089/list``

``docker container logs --tail 4 todo-dev-todo-web-1``
