pipeline {
  environment {
    registry = "asemn00"
    image_name = "gpn-test"
    registryCredential = 'docker-hub'
    dockerImage = ''
  }
  agent {label 'localhost'}
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/asemnurzhanova/test-task.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build "$registry/$image_name:$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry/$image_name:$BUILD_NUMBER"
      }
    }
  }
}
