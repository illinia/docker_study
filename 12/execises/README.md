### 12.2 도커 스웜으로 클러스터 만들기

``docker swarm join-token worker``

``docker swarm join-token manager``

``docker node ls``

### 12.3 도커 스웜 서비스로 애플리케이션 실행하기

``docker service create --name timecheck --replicas 1 diamol/ch12-timecheck:1.0``

``docker service ls``

``docker service ps timecheck``

``docker container ls``

``docker container rm -f $(docker container ls --last 1 -q)``

``docker service ps timecheck``

``docker serivce logs --since 10s timecheck``

``docker service inspect timecheck -f '{{.Spec.TaskTemplate.ContainerSpec.Image}}'``

``docker service update --image diamol/ch12-timecheck:2.0 timecheck``

``docker service ps timecheck``

``docker service logs --since 20s timecheck``

``docker service update --rollback timecheck``

``docker service ps timecheck``

``docker service logs --since 25s timecheck``

### 12.4 클러스터 환경에서 네트워크 트래픽 관리하기

``docker service rm timecheck``

``docker network create --driver overlay iotd-net``

``docker service create --detach --replicas 3 --network iotd-net --name iotd diamol/ch09-image-of-the-day``

``docker service create --detach --replicas 2 --network iotd-net --name accesslog diamol/ch09-access-log``

``docker service ls``

``docker container exec -it $(docker container ls --last 1 -q) sh``

``nslookup iotd``

``nslookup accesslog``

``docker service create --detach --name image-gallery --network iotd-net --publish 8010:80 --replicas 2 diamol/ch09-image-gallery``

``docker service ls``

### 12.6 연습문제

``docker network create --driver overlay numbers``

``docker service create --detach --replicas 3 --network numbers --name numbers-api diamol/ch08-numbers-api:v3``

``docker service create --detach --name numbers-web --network numbers --publish 8020:80 --replicas 3 diamol/ch08-numbers-web:v3``