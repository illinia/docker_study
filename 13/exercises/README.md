### 13.1 도커 컴포즈를 사용한 운영 환경

``docker stack deploy -c ./todo-list/v1.yml todo``

``docker stack ls``

``docker service ls``

``docker stack deploy -c ./todo-list/v2.yml todo``

``docker service ps todo_todo-web``

``docker stack services todo``

``docker stack ps todo``

``docker stack rm todo``

### 13.2 컨피그 객체를 이용한 설정값 관리

``docker config create todo-list-config ./todo-list/configs/config.json``

``docker config ls``

``docker config inspect --pretty todo-list-config``

``docker stack deploy -c ./todo-list/v3.yml todo``

``docker stack services todo``

### 13.3 비밀값을 이용한 대외비 설정 정보 관리하기

``docker secret create todo-list-secret ./todo-list/secrets/secrets.json``

``docker secret inspect --pretty todo-list-secret``

``docker stack deploy -c ./todo-list/v4.yml todo``

``docker stack ps todo``

### 13.4 스웜에서 볼륨 사용하기

``docker node udpate --label-add storage=raid $(docker node ls -q)``

``docker volume ls -q``

``docker stack deploy -c ./todo-list/v5.yml todo``

``docker volume ls -q``

``docker stack deploy -c ./todo-list/v6.yml todo``

``docker stack ps todo``

``docker volume ls -q``