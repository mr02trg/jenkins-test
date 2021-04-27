pipeline {
    agent any
    stages {
        stage('performance testing') {
            agent {
                docker {
                    image 'justb4/jmeter:latest'
                    args "--entrypoint=''"
                }
            }
            environment {
                HOST= "smh.com.au"
            }
            steps {
                sh "ls -la"
                sh "jmeter --version"
                sh 'jmeter -n -t jmeter/TestPlan.jmx -JHOST="${HOST}" -l jmeter/TestResult-${BUILD_NUMBER}.jlt'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: "jmeter/TestResult-${BUILD_NUMBER}.jlt", fingerprint: true
        }
    }
}