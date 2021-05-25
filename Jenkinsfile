pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh ("./script/assign-env.sh")
      }
    }
    stage('Test') {
      steps {
        echo '${env.DEPLOY_STATUS}'
      }
    }
  }
}