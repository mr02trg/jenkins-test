pipeline {
  agent any

  environment {
		DEPLOY_STATUS_FILE = 'deploy_status.txt'
		PATH = "${env.WORKSPACE}/node_modules/.bin:${env.PATH}"
	}

  stages {
    stage('Build') {
      steps {
        sh('./script/assign-env.sh')
        script {
          if (fileExists(env.DEPLOY_STATUS_FILE)) {
            env.DEPLOY_STATUS = readFile(env.DEPLOY_STATUS_FILE).trim()
          } else {
            env.DEPLOY_STATUS = "NO_DEPLOY"
          }
        }
      }
    }
    stage('DAST') {
      when { expression { DEPLOY_STATUS == 'DEPLOY_SUCCESS' } }
      environment {
        SFDX_VAR = "Tue"
      }
			steps {
        echo "${env.DEPLOY_STATUS}"
				sshagent(['zapserver']){
          sh 'echo "Hello ${SFDX_VAR} from zap"'
					// sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.239.5.223 "sudo docker run -v /home/ubuntu/butn_report:/zap/wrk/:rw -t owasp/zap2docker-stable zap-baseline.py -t ${SFDX_VAR} -c ./zap-baseline.conf -r ./report.html || if [ $? -ne 1 ]; then exit 0; else exit 1; fi;"'
					// sh 'scp ubuntu@13.239.5.223:/home/ubuntu/butn_report/report.html ./zap-report.html'
				}
			}
		}
  }
  post {
		cleanup {
			cleanWs()
		}
	}
}