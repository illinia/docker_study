### 19.1 표준 에러 스트림과 표준 출력 스트림

``docker container run diamol/ch15-timecheck:3.0``

``docker container run -d --name timecheck diamol/ch15-timecheck:3.0``

``docker container logs --tail 1 timecheck``

``docker container stop timecheck``

``docker container logs --tail 1 timecheck``

``docker container inspect --format='{{.LogPath}}' timecheck``

``docker container run -d --name timecheck2 --log-opt max-size=5k --log-opt max-file=3 -e Timer__IntervalSeconds=1 diamol/ch15-timecheck:3.0``

``docker container inspect --format='{{.LogPath}}' timecheck2``

### 19.2 다른 곳으로 출력된 로그를 stdout 스트림에 전달하기

``docker container run -d --name timecheck3 diamol/ch19-timecheck:4.0``

``docker container logs timecheck3``

``docker container exec -it timecheck3 sh``

``cat /logs/timecheck.log``

``docker container run -d --name timecheck4 diamol/ch19-timecheck:5.0``

``docker container logs timecheck4``

``docker container exec -it timecheck4 sh``
