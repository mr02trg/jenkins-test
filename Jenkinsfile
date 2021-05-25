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
    stage('DAST') {
			steps {
				sshagent(['zapserver']){
          echo "Hello world from zap"
          echo "${env.custom_var}"
					// sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.239.5.223 "sudo docker run -v /home/ubuntu/butn_report:/zap/wrk/:rw -t owasp/zap2docker-stable zap-baseline.py -t https://aggsandbox-poc.cs113.force.com/bp/s -c ./zap-baseline.conf -r ./report.html || if [ $? -ne 1 ]; then exit 0; else exit 1; fi;"'
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