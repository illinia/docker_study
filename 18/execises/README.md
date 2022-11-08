### 18.1 다단 애플리케이션 설정

/access-log

``docker container run -d -p 8080:80 diamol/ch18-access-log``

``docker container run -d -p 8081:80 -v "$(pwd)/config/dev:/app/configoverride" diamol/ch18-access-log``

``curl http://localhost:8080/config``

``curl http://localhost:8081/config``

``docker container run -d -p 8082:80 -v "$(pwd)/config/dev:/app/config-override" -e NODE_CONFIG='{\"metrics\": {\"enabled\":\"true\"}}' diamol/ch18-access-log``

``curl http://localhost:8082/config``

### 18.2 환경별 설정 패키징하기

``docker container run -d -p 8083:80 diamol/ch18-todo-list``

``docker container run -d -p 8084:80 -e DOTNET_ENVIRONMENT=Test diamol/ch18-todo-list``

``docker container run -d -p 8085:80 -e DOTNET_ENVIRONMENT=Production -v "$(pwd)/config/prod-local:/app/config-override" diamol/ch18-todo-list``

### 18.3 런타임에서 설정 읽어 들이기

``docker container run -d -p 8060:80 diamol/ch18-image-gallery``

``curl http://localhost:8086/config``

``docker container run -d -p 8087:80 -v "$(pwd)/config/dev:/app/config-override" diamol/ch18-image-gallery``

``curl http://localhost:8087/config``

``docker container run -d -p 8088:80 -v "$(pwd)/config/dev:/app/config-override" -e IG_METRICS.ENABLED=TRUE diamol/ch18-image-gallery``

``curl http://localhost:8088/config``

### 18.4 레거시 애플리케이션 설정 전략 적용하기

/image-of-the-day

``docker container run -d -p 8089:80 diamol/ch18-image-of-the-day``

``docker container run -d -p 8090:80 -v "$(pwd)/config/dev:/config-override" -e CONFIG_SOURCE_PATH="/config-override/application.properties" diamol/ch18-image-of-the-day``

``docker container rm -f $(docker container ls -aq)``

``docker-compose up -d``

