pipeline {  
    environment {
    registry = "anandsingh555/docker-images"
    registryCredential = 'dockerhubcred'
  }  
  agent any  
  stages {
    stage('Building image') {
      steps{
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
  }
}
