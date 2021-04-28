pipeline {
    agent any
    stages {
        stage('begin') {
            steps{
                echo "Begin..."
            }
        }
        stage('checkout') {
            steps{
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    userRemoteConfigs: [[url: 'https://github.com/mr02trg/jenkins-test.git']]
                ])
            }
        }
        stage('performance testing') {
            agent {
                docker {
                    image 'justb4/jmeter:latest'
                    args "--entrypoint=''"
                    reuseNode true
                }
            }
            environment {
                HOST= "smh.com.au"
            }
            steps {
                sh "ls -la"
                sh "jmeter --version"
                sh 'jmeter -n -t jmeter-resources/TestPlan.jmx -JHOST="${HOST}" -Jjmeter.save.saveservice.output_format=xml -l jmeter-resources/TestResult-${BUILD_NUMBER}.jlt'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: "jmeter-resources/TestResult-${BUILD_NUMBER}.jlt", fingerprint: true
        }
        success {
            perfReport(
                sourceDataFiles: "jmeter-resources/TestResult-${BUILD_NUMBER}.jlt",
                errorUnstableThreshold: 1,
                errorFailedThreshold: 3
            )
        }
        cleanup {
            echo "Cleaned Up Workspace For Project"
			cleanWs()
		}
    }
}