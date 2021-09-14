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
        sh 'docker build -t $imagename:version1 .'
      }
    }
    stage('Deploy Image') {
      steps {
        script{
          docker.withRegistry('', registryCredential) {
            dockerImage.push("$BUILD_NUMBER")
            dockerImage.push('v1')
          }
        }
      }
    }
  }
}
