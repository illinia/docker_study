### 15.1 도커 API 의 엔드 포인트 형태

daemon.json 파일 수정하여 비보안 http 접근 허용하기

{
    "hosts": [
        "tcp://0.0.0.0:2375",
        "fd://"
    ],
    "insecure-registries": [
        "registry.local:5000"
    ]
}

``docker --host tcp://localhost:2375 container ls``

``curl http://localhost:2375/containers/json``

``docker --host tcp://localhost:2375 container run -it -v /:/host-drive diamol/base``

### 15.2 보안 원격 접근을 위한 도커 엔진

play with docker 에 로그인 후 노드 생성

``mkdir -p /diamol-certs``

``docker container run -v /diamol-certs:/certs -v /etc/docker:/docker dimaol/pwd-tls:server``

``pkill dockerd``

``dockerd &>/docker.log &``

``pwdDomain="현재 세션 pwd 도메인"``

``curl "http://$pwdDomain/containers/json"``

``docker --host "tcp://$pwdDomain" container ls``

``mkdir -p /tmp/pwd-certs``

``cd ./ch15/exercises``

``tar -xvf pwd-client-certs -C /tmp/pwd-certs``

``docker --host "tcp://$pwdDomain" --tlsverify --tlscacert /tmp/pwd-certs/ca.pem --tlscert /tmp/pwd-certs/client-cert.pem --tlskey /tmp/pwd-certs/client-key.pem container ls``

``docker --host "tcp://$pwdDomain" --tlsverify --tlscacert /tmp/pwd-certs/ca.pem --tlscert /tmp/pwd-certs/client-cert.pem --tlskey /tmp/pwd-certs/client-key.pem container run -d -P diamol/apache``

### 15.3 도커 컨텍스트를 사용해 원격 엔진에서 작업하기

``export DOCKER_CONTEXT='pwd-tls'``

``docker context ls``

``docker container ls``

``docker context use default``

``docker container ls``

### 15.4 지속적 통합 파이프라인에 지속적 배포 추가하기

``docker-compose -f ./docker-compose.yml -f ./docker-compose-linux.yml up -d``

Jenkinsfile 에 environment 값의 UAT_ENGINE, PROD_ENGINE 변수값을 play with docker 도메인 + 80 포트로 추가
80 포트 주시하다 들어오는 트래픽을 play with docker 2376 포트로 연결해줌.

``git remote add ch15 http://localhost:3000/diamol/diamol.git``

``git commit -a -m 'Play with Docker 도메인 정보 추가'``

``git push ch15``

