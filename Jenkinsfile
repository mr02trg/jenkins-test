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
        sh('echo ${?}')
        sh('echo ${DEPLOY_STATUS}')
      }
    }
  }
}