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
        script {
        def dockerRun = 'docker run -p 8080:8080 -d --name my-app ${env.registry} + ":$BUILD_NUMBER"'
      }
      }
   }

    stage('Remove Unused docker image') {
      steps {
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
