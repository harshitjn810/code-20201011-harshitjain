pipeline {
   agent none
    stages {
        stage('Build') {
            agent {
                docker {
                     image 'python:2-alpine'
                }
            }
            steps {
                sh 'python -m py_compile src.py bmi_cal.py'
                stash(name: 'compiled-results', includes: '*.py*')
            }
        }
        stage('Test') {
            agent {
                docker {
                       image 'qnib/pytest'
                }
            }
            steps {
                    sh 'py.test --verbose --junit-xml test-reports/results.xml test.py'
            }
    }
}
}
