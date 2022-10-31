### 5.2 도커 허브에 직접 빌드한 이미지 푸시하기
``export dockerId=도커허브계정이름``

``docker login --username $dockerId``

``docker image tag image-gallery $dockerId/image-gallery:v1``

``docker image ls --filter reference=image-gallery --filter reference='*/image-gallery'``

``docker image push $dockerId/image-gallery:v1``

### 5.3 나만의 도커 레지스트리 운영하기
``docker container run -d -p 5001:5001 --restart always diamol/registry``

``echo $'\n127.0.0.1 registry.local' | sudo tee -a /etc/hosts``

daemon.json 에 추가
``{"insecure-registries" : ["registry.local:5001"]}``

``docker info``

``docker image push registry.local:5001/gallery/ui:v1``

### 5.4 이미지 태그를 효율적으로 사용하기

``docker image tag image-gallery registry.local:5001/gallery/ui:latest``
``docker image tag image-gallery registry.local:5001/gallery/ui:2``
``docker image tag image-gallery registry.local:5001/gallery/ui:2.1``
``docker image tag image-gallery registry.local:5001/gallery/ui:2.1.106``

### 5.5 공식 이미지에서 골든 이미지로 전환하기

``docker image build -t golden/dotnetcore-sdk:3.0 .``

``docker image build -t golden/aspnet-core:3.0 .``