### 2.1 컨테이너로 Hello World 실행하기
도커 컨테이너 실행하기
``docker container run diamol/ch02-hello-diamol``

같은 명령어 한번더 실행
``docker container run diamol/ch02-hello-diamol``

### 2.3 컨테이너를 원격 컴퓨터처럼 사용하기
``docker container run --interactive --tty diamol/base``

``docker container ls``

특정 컨테이너 특정
``docker container top 특정이름``

로그 수집
``docker container logs 특정이름``

### 2.4 컨테이너를 사용해 웹 사이트 호스팅하기
``docker container run --detach --publish 8088:80 diamol/ch02-hello-diamol-web``

컨테이너 상태 확인
``docker container stats 특정이름``

모든 컨테이너 확인 후 삭제
``docker container rm --force $(docker container ls --all --quiet)``

### 실습
웹 사이트 컨테이너를 실행하고 index.html 파일을 교체해 웹 페이지 내용 수정
``docker container run --detach --publish 8088:80 diamol/ch02-hello-diamol-web``

``docker container ps``

``docker exec -it 컨테이너이름 /bin/sh``

이후 index.html 디렉토리까지 이동해서 수정