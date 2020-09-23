pipeline {
    agent { 
        label 'asus'
    }
    stages {
        stage('Build') {
            steps {
                sh 'python3 -m py_compile sources/add2vals.py sources/calc.py'
            }
        }
        stage('Test') {
            steps {
                sh 'python3 -m pytest --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh 'python3 -m PyInstaller sources/add2vals.py'
            }
            post {
                success {
                    archiveArtifacts 'build/add2vals'
                }
            }
        }
    }
}
