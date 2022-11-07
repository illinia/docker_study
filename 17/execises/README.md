### 17.1 도커 이미지를 최적화하는 방법

``docker image build -t diamol/ch17-build-context:v1 .``

``docker image build -t diamol/ch17-build-context:v2 -f ./Dockerfile.v2 .``

``docker imgae ls``

### 17.2 좋은 기반 이미지를 고르는 법

``docker image build -t diamol/ch17-truth-app .``

``docker container run -d -p 8010:80 --name truth diamol/ch17-truth-app``

``curl http://localhost:8010/truth``

``docker container exec -it truth sh``

``docker container exec -it truth cmd``

``javac FileUpdateTest.java``

``java FileUpdateTest``

``exit``

``curl http://localhost:8010/truth``

앤코어 ch17/execises/anchore

``docker-compose up -d``

``docker exec anchore-engine-api-a anchore-cli system wait``

``docker container cp "./openjdk/Dockerfile" anchore-engine-api-1:/Dockerfile``

``docker container exec anchore-engine-api-1 anchore-cli image add diamol/openjdk --dockerfile /Dockerfile``

``docker container exec anchore-engine-api-1 anchore-cli image wait diamol/openjdk``

``docker container exec anchore-engine-api-1 anchore-cli image content diamol/openjdk java``

``docker container exec anchore-engine-api-1 anchore-cli image vuln diamol/openjdk all``

### 17.3 이미지 레이어 수와 이미지 크기는 최소한으로

``docker image build -t diamol/ch17-socat:v1 .``

``docker image build -t diamol/ch17-socat:v2 -f Dockerfile.v2 .``

``docker image ls -f reference=diamol/ch17-socat``

ch17/exercises/ml-dataset

``docker image build -t diamol/ch17-ml-dataset:v1 .``

``docker image build -t diamol/ch17-ml-dataset:v2 -f Dockerfile.v2 .``

``docker image ls -f reference=diamol/ch17-ml-dataset``

### 17.4 멀티 스테이지 빌드를 한 단계 업그레이드하기

``docker image build -t diamol/ch17-ml-dataset:v3 -f Dockerfile.v3 .``

``docker image build -t diamol/ch17-ml-dataset:v3-download -f Dockerfile.v3 --target download .``

``docker image build -t diamol/ch17-ml-dataset:v3-expand -f Dockerfile.v3 --target expand .``

``docker image ls -f reference=diamol/ch17-ml-dataset``

/jenkins

``docker image build -t diamol/ch17-jenkins:v1 .``

``docker image build -t diamol/ch17-jenkins:v2 -f Dockerfile.v2 .``

``echo 2.0 > jenkins.install.UpgradeWizard.state``

``docker image build -t diamol/ch17-jenkins:v1 .``

``docker image build -t diamol/ch17-jenkins:v2 -f Dockerfile.v2 .``