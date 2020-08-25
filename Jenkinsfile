def IMAGE_NAME01="jenkins-pipeline"
def IMAGE_TAG01="latest"
def IMAGE_NAME02="jenkins/jenkins"
def IMAGE_TAG2="lts"
def IOTYPE="docker.io"
def DOCKERHUB_USER="egbea123"
def DPass="Zuft@08caring"
def DOCKER_REGISTRY ="egbea123/jenkins-image"
def Git_clone='github.com/egbea123/jenkins-pipeline.git'

pipeline {
 environment {
    registry = "egbea123/jenkins-image"
    registryCredential = "dockerhub"
  }
   agent any

  stages {
       stage('Cloning Git') {
      steps {
        git 'https://github.com/egbea123/jenkins-pipeline.git'
      }
    }
     stage('docker-compose') {
        steps{
          echo "buiding images"
          sh 'rundockerbuild.sh'
           echo "Image build complete"
          }
       } 
     
      stage('deploy') {
        steps {
          echo "Pushing image1 to GitHub registry"
          sh 'sudo docker login -u $DOCKERHUB_USER -p $DPass'
          sh 'sudo docker tag  $IMAGE_NAME01:$IMAGE_TAG01 $IOTYPE/$DOCKER_REGISTRY/$IMAGE_NAME01:$IMAGE_TAG01'
          sh 'sudo docker push $DOCKER_RRGISTRY/$IMAGE_NAME01:$IMAGE_TAG01'
          echo "Image push image1 complete"
          
          echo "Pushing image2 to GitHub registry"
          sh 'docker tag  $IMAGE_NAME02:$IMAGE_TAG02 $IOTYPE/$DOCKER_REGISTRY/$IMAGE_NAME02:$IMAGE_TAG02'
          sh 'docker push $DOCKER_RRGISTRY/$IMAGE_NAME02:$IMAGE_TAG02'
          echo "Image push image2 complete"
      }
    }  
  }
  post{
      always {
         sh 'sduo docker-compose down || true'
      }
   }   
}
