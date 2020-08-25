def IMAGE_NAME01="jenkins-pipeline"
def IMAGE_TAG01="latest"
def IMAGE_NAME02="jenkins/jenkins"
def IMAGE_TAG2="lts"
def DockerTYPE="docker.io"
def DOCKER_HUB_USER="egbea123"
def DOCKERPass="Zuft@08caring"
def DOCKER_RRGISTRY ="egbea123/jenkins-image"
def Git_clone="github.com/egbea123/jenkins-pipeline.git"

pipeline {
 environment {
    registry = "egbea123/jenkins-image"
    registryCredential = "dockerhub"
  }
   agent any

  stages {
       stage('Cloning Git') {
      steps {
        git 'https://Git_clone'
      }
    }
     stage('docker-compose') {
        steps{
          echo "buiding images"
          sh "docker-compose build"
          sh "docker-compose up -d"
          echo "Image build complete"
          }
       } 
     
      stage('deploy') {
        steps {
          echo "Pushing image1 to GitHub registry"
          sh "docker login -u $DOCKER_HUB_USER -p $DOCKER_Pass"
          sh "docker tag  $IMAGE_NAME01:$IMAGE_TAG01 $Docker_TYPE/$DOCKERR_RRGISTRY/$IMAGE_NAME01:$IMAGE_TAG01"
          sh "docker push $DOCKER_RRGISTRY/$IMAGE_NAME01:$IMAGE_TAG01"
          echo "Image push image1 complete"
          
          echo "Pushing image2 to GitHub registry"
          sh "docker tag  $IMAGE_NAME02:$IMAGE_TAG02 $Docker_TYPE/$DOCKERR_RRGISTRY/$IMAGE_NAME02:$IMAGE_TAG02"
          sh "docker push $DOCKERR_RRGISTRY/$IMAGE_NAME02:$IMAGE_TAG02"
          echo "Image push image2 complete"
      }
    }  
  }
  post{
      always {
         sh "docker-compose down || true"
      }
   }   
}
