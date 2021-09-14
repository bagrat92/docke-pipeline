pipeline {
  environment {
    imagename = "bagrat92/ubuntu"
    registryCredential = 'docker_id'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git Repo') {
      steps {
        git([url: 'git@github.com:bagrat92/docke-pipeline.git', branch: 'main', credentialsId: 'github_ssh_key'])
      }
    }
    stage('Building image') {
      steps {
        script{
          dockerImage = docker.build("$imagename:version3") .
        }
      }
    }
    stage('Deploy Image') {
      steps {
        script{
          docker.withRegistry('https://hub.docker.com/repository/docker/bagrat92/ubuntu', registryCredential) {
            dockerImage.push("$BUILD_NUMBER")
            dockerImage.push('v1')
          }
        }
      }
    }
  }
}
