pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh('./script/assign-env.sh')
        script {
          tmp_param = readFile('deploy_status.txt').trim()
          env.custom_var = tmp_param
        }
      }
    }
    stage('Test') {
      steps {
        echo "${env.custom_var}"
      }
    }
  }
  post {
		cleanup {
			cleanWs()
		}
	}
}