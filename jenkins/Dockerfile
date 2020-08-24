FROM jenkins/jenkins:lts
#Switch user to root, let the the entrypoint drop back to jenkins
USER root

#Install debian packages, gosu, and dockerRUN apt-get update && \
RUN apt-get update && \ 
    DEBIAN_FRONTEND=noninteractive \ 
    apt-get -y install apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common && \
curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
     add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
    $(lsb_release -cs) \
    stable" && \
apt-get update && \
apt-get -y install docker-ce
RUN apt-get install -y docker-ce

RUN usermod -a -G docker jenkins
USER jenkins
