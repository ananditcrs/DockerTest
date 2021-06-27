pipeline {  

  environment {
    registry = "anandsingh555/docker-images"
    registryCredential = 'dockerhubcred'
    dockerImage = ''
  }

  agent any  
  stages {
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry('', registryCredential) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Run Container on Dev Server'){
      steps {
          sh "docker run -p 80:80 -d --name my-app $registry:$BUILD_NUMBER"
      }
   }

    stage('Remove Unused docker image') {
      steps {
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
