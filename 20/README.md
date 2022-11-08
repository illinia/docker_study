### 20.1 리버스 프록시란?

``docker network create ch20``

``docker-compose -f nginx/docker-compose.yml -f nginx/override-linux.yml up -d``

``echo $'\n127.0.0.1 whoami.local' | sudo tee -a /etc/hosts``

``docker-compose -f whoami/docker-compose.yml up -d``

``cp ./nginx/sites-available/whoami.local ./nginx/sites-enabled/``

``docker-compose -f nginx/docker-compose.yml restart nginx``

``echo $'\n127.0.0.1 api.numbers.local' | sudo tee -a /etc/hosts``

``docker-compose -f numbers/docker-compose.yml up -d``

``cp ./nginx/sites-available/api.numbers.local ./nginx/sites-enabled/``

``docker-compose -f nginx/docker-compose.yml restart nginx``

### 20.2 리버스 프록시의 라우팅과 SSL 적용하기

``echo $'\n127.0.0.1 image-gallery.local' | sudo tee -a /etc/hosts``

``docker-compose -f ./image-gallery/docker-compose.yml up -d --scale image-gallery=3``

``cp ./nginx/sites-available/image-gallery.local ./nginx/sites-enabled/``

``docker-compose -f ./nginx/docker-compose.yml restart nginx``

``curl -i --head http://image-gallery.local``

``rm ./nginx/sites-enabled/image-gallery.local``

``cp ./nginx/sites-available/image-gallery-2.local ./nginx/sites-enabled/image-gallery.local``

``docker-compose -f ./nginx/docker-compose.yml restart nginx``

``curl -i http://image-gallery.local/api/image``

``docker container run -v "$(pwd)/nginx/certs:/certs" -e HOST_NAME=image-gallery.local diamol/cert-generator``

### 20.3 프록시를 이용한 성능 및 신뢰성 개선

``rm ./nginx/sites-enabled/image-gallery.local``

``cp ./nginx/sites-available/image-gallery-4.local ./nginx/sites-enabled/image-gallery.local``

``docker-compose -f ./nginx/docker-compose.yml restart nginx``

2번 실행

``curl -i --head --insecure https://image-gallery.local``

### 20.4 클라우드 네이티브 리버스 프록시

``docker container rm -f $(docker container ls -aq)``

``docker-compose -f traefik/docker-compose.yml -f traefik/override-linux.yml up -d``

``docker-compose -f whoami/docker-compose.yml -f whoami/override-traefik.yml up -d``

``curl -i http://whoami.local``

``docker-compose -f image-gallery/docker-compose.yml -f image-gallery/override-traefik-ssl.yml up -d``

``curl --head --insecure https://image-gallery.local``

``curl --insecure https://image-gallery.local/api/image``

``docker-compose -f whoami/docker-compose.yml -f whoami/override-traefik.yml up -d --scale whoami=3``

2 번 실행

``curl -c c.txt -b c.txt http://whoami.local``

``docker-compose -f whoami/docker-compose.yml -f whoami/override-traefik-sticky.yml up -d --scale whoami=3``

2 번 실행

``curl -c c.txt -b c.txt http://whoami.local``