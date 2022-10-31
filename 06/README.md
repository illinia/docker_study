### 6.1 컨테이너 속 데이터가 사라지는 이유

``docker container run --name rn1 diamol/ch06-random-number``

``docker container run --name rn2 diamol/ch06-random-number``

``docker container cp rn1:/random/number.txt number1.txt``

``docker container cp rn2:/random/number.txt number2.txt``

``cat number1.txt``
``cat number2.txt``

``docker container run --name f1 diamol/ch06-file-display``

``echo "http://eltonstoneman.com" > url.txt``

``docker container cp url.txt f1:/input.txt``

``docker container start --attach f1``

``docker container run --name f2 diamol/ch06-file-display``

``docker container rm -f f1``

``docker container cp f1:/input.txt .``

### 6.2 도커 볼륨을 사용하는 컨테이너 실행하기

``docker container run --name todo1 -d -p 8010:80 diamol/ch06-todo-list``

``docker container inspect --format '{{.Mounts}}' todo1``

``docker volume ls``

``docker container run --name todo2 -d diamol/ch06-todo-list``

``docker container exec todo2 ls /data``

``docker container run -d --name t3 --volumes-from todo1 diamol/ch06-todo-list``

``docker container exec t3 ls /data``

### 6.3 파일 시스템 마운트를 사용하는 컨테이너 실행하기

``source="$(pwd)/databases" && taret='/data'``

``mkdir ./databases``

``docker container run --mount type=bind,source=$source,target=$target -d -p 8012:80 diamol/ch06-todo-list``

``curl http://localhost:8012``

``ls ./databases``

예제 소스 코드 /ch06/exercises/todo-list 에서
``source="$(pwd)/config" && target='/app/config'``

``docker container run --name todo-configured -d -p 8013:80 --mount type=bind,source=$source,target=$target,readonly diamol/ch06-todo-list``

``curl http://localhost:8013``

``docker container logs todo-configured``

### 6.4 파일 시스템 마운트의 한계점

``source="$(pwd)/new" && target='/init``

``docker container run diamol/ch06-bind-mount``

``docker container run --mount type=bind,source=$source,target=$target diamol/ch06-bind-mount``
