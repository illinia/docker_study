### 14.1 도커를 사용한 애플리케이션 업그레이드 프로세스

병합이 재대로 안되는 버그 있음, 병합 된 컴포즈 파일 버젼을 지정해줘야 함

``docker-compose -f ./numbers/docker-compose.yml -f ./numbers/prod.yml config > stack.yml``

``docker stack deploy -c stack.yml numbers``

``docker stack services numbers``

``docker-compose -f ./numbers/docker-compose.yml -f ./numbers/prod.yml -f ./numbers/prod-healthcheck.yml -f ./numbers/v2.yml config > stack.yml``

``docker stack deploy -c stack.yml numbers``

``docker stack ps numbers``

### 14.2 운영 환경을 위한 롤링 업데이트 설정하기

``docker-compose -f ./numbers/docker-compose.yml -f ./numbers/prod.yml -f ./numbers/prod-healthcheck.yml -f ./numbers/prod-update-config.yml -f ./numbers/v3.yml config > stack.yml``

``docker stack deploy -c stack.yml numbers``

``docker stack ps numbers``

``docker-compose -f ./numbers/docker-compose.yml -f ./numbers/prod.yml -f ./numbers/prod-healthcheck.yml -f ./numbers/prod-update-config.yml -f ./numbers/v5-bad.yml config > stack.yml``

``docker stack deploy -c stack.yml numbers``

``docker service inspect --pretty nubmers_numbers-api``

``docker-compose -f ./numbers/docker-compose.yml -f ./numbers/prod-full.yml -f ./numbers/v5.yml config > stack.yml``

``docker stack deploy -c stack.yml numbers``

``docker service inspect --pretty nubmers_numbers-api``

### 14.4 클러스터의 중단 시간

play with docker 사이트에서 진행

인스턴스 5개 생성

``ip=$(hostname -i)``

``docker swarm init --advertise-addr $ip``

``docker swarm join-token manager``

``docker swarm join-token worker``

node2, node3 에 매니저 노드 추가 명령 입력
node4, node5 에 매니저 노드 추가 명령 입력

``docker node ls``

``docker node update --availability drain node5``

``docker node update --availability drain node3``

``docker node ls``

``docker swarm leave --force``

``docker node update --availability active node5``

``docker node promote node5``

``docker node ls``

