``docker container rm -f $(docker container ls -aq)``

``docker image rm -f $(docker image ls -f reference='diamol/*' -q)``