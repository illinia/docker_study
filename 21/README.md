### 21.1 비동기 메시징이란?

``docker network create ch21``

``docker container run -d --name redis --network ch21 diamol/redis``

``docker container logs redis --tail 1``

``docker run -d --name publisher --network ch21 diamol/redis-cli -r 50 -i 5 PUBLISH channel21 ping``

``docker run -it --network ch21 --name subscriber diamol/redis-cli SUBSCRIBE channel21``

### 21.2 클라우드 네이티브 메시지 큐 사용하기

todo-list

``docker-compose up -d message-queue``

``docker container logs todo-list-message-queue-1``

``curl http://localhost:8222/connz``

``docker-compose up -d todo-web todo-db``

``docker container run -d --name todo-sub --network todo-list-app-net diamol/nats-sub events.todo.newitem``

``docker container logs todo-sub``

### 21.3 메시지 수신 및 처리

``docker-compose up -d save-handler``

``docker logs todo-list-save-handler-1``

``docker-compose up -d --scale save-handler=3``

``docker logs todo-list-save-handler-2``

``docker-compose logs --tail=1 save-handler``

### 21.4 메시지 핸들러로 기능 추가하기

``docker-compose -f docker-composeyml -f docker-compose-audit.yml up -d --scale save-handler=3``

``docker logs todo-list-audit-handler-1``

