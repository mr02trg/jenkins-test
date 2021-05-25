pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        tmp_param = sh (script: "./script/assign-env.sh", returnStdout: true).trim()
        env.custom_var = tmp_param
      }
    }
    stage('Test') {
      steps {
        echo "${env.custom_var}"
      }
    }
  }
}