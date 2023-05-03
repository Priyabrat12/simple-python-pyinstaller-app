pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }
        stage('Test') {
            steps {
                sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit 'skipPublishingChecks: true, test-reports/results.xml'
                    sh "cat /var/lib/jenkins/workspace/simple-python-pyinstaller-app/test-reports/results.xml'
                }
            }
        }
    }
}
