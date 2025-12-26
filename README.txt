Run Docker Image -

docker network create jenkins

docker run --name jenkins-docker --rm --detach \
  --privileged --network jenkins --network-alias docker \
  --env DOCKER_TLS_CERTDIR=/certs \
  --volume jenkins-docker-certs:/certs/client \
  --volume jenkins_home:/var/jenkins_home \
  --publish 2376:2376 \
  docker:dind --storage-driver overlay2

  
docker run -d \
  --name jenkins-dind \
  --restart=on-failure \
  --privileged \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  -p 8080:8080 \
  -p 50000:50000 \
  --volume jenkins_home:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  jenkins-dind

Install dependency -

docker exec -u root -it jenkins-dind bash
apt update -y
apt install -y python3
python3 --version
ln -s /usr/bin/python3 /usr/bin/python
python --version
apt install -y python3-pip
apt install -y python3-venv
exit

Restart Jenkins -
docker restart jenkins-dind

