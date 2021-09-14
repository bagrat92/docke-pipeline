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
        git([url: 'git@github.com:bagrat92/docker-pipeline.git', branch: 'master', credentialId: 'github_ssh_key'])
      }
    }
    stage('Building image') {
      steps {
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Deploy Image') {
      steps {
        script{
          docker.withRegistry('', registryCredential) {
            dockerImage.push("$BUILD_NUMBER")
            dockerImage.push('v2')
          }
        }
      }
    }
  }
}
