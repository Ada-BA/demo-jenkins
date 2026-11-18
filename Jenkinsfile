pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }
        stage('Tests') {
            steps {
                sh './venv/bin/pytest --junitxml=report.xml'
            }
            post {
                always { junit 'report.xml' }
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'app.py', fingerprint: true
            }
        }
    }
    post {
        success { echo 'Pipeline réussi' }
        failure { echo 'Pipeline en échec' }
    }
}
