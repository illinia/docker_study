### 16.1 다중 아키텍처 이미지가 중요한 이유

도커 데스크탑에서 daemin.json 수정
{
    "experimental": true
}

``docker build -t diamol/ch16-whoami:linux-arm64 --platform linux/arm64 ./whoami``

``docker image inspect diamol/ch16-whoami:linux-arm64 -f '{{.Os}}/{{.Architecture}}'``

``docker info -f '{{.OSType}}/{{.Architecture}}'``

### 16.2 다중 아키텍처 이미지를 만들기 위한 Dockerfile 스크립트

``docker image build -t diamol/ch16-folder-list:linux-amd64 -f ./Dockerfile.linux-amd64 .``

``docker image build -t diamol/ch16-folder-list:linux-arm64 -f ./Dockerfile.linux-arm64 --platform linux/arm64 .``

``docker image build -t diamol/ch16-folder-list:linux-arm -f ./Dockerfile.linux-arm --platform linux/arm .``

``docker container run diamol/ch16-folder-list:linux-amd64``

``docker container run diamol/ch16-folder-list:linux-arm64``

``docker container run diamol/ch16-folder-list:linux-arm``

``docker image build -t diamol/ch16-folder-list .``

``docker container run diamol/ch16-folder-list``

### 16.3 다중 아키텍처 이미지를 레지스트리에 푸시하기

``dockerId='도커허브 계정'``

``docker image tag diamol/ch16-folder-list:linux-amd64 "$dockerId/ch16-folder-list:linux-amd64"``

``docker image tag diamol/ch16-folder-list:linux-arm64 "$dockerId/ch16-folder-list:linux-arm64"``

``docker image tag diamol/ch16-folder-list:linux-arm "$dockerId/ch16-folder-list:linux-arm"``

``docker image push "$dockerId/ch16-folder-list" -a``

``docker manifest inspect diamol/base``

``docker manifest create "$dockerId/ch16-folder-list" "$dockerId/ch16-folder-list:linux-amd64" "$dockerId/ch16-folder-list:linux-arm64" "$dockerId/ch16-folder-list:linux-arm"``

``docker manifest push "$dockerId/ch16-folder-list"``

### 16.4 도커 Buildx를 사용해 다중 아키텍처 이미지 빌드하기

``node2ip=노드2의_ip``

``ssh $node2ip``

``exit``

``docker context create node1 --docker "host=unix:///var/run/docker.sock"``

``docker context create node2 --docker "host=ssh://root@$node2ip"``

``docker context ls``

