pipeline {
    agent none
    stages {
        stage('performance testing') {
            agent {
                docker {
                    image 'justb4/jmeter:latest'
                    args '-v ${PWD}/jmeter:${PWD} -w ${PWD}'
                }
            }
            environment {
                HOST= "smh.com.au"
            }
            steps {
                sh 'jmeter -n -t TestPlan.jmx -JHOST="${HOST}" -l TestResult-${BUILD_NUMBER}.jlt'
            }
        }
    }
}

