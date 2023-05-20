pipeline {
    agent any
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'java -version'
            }
        }
        stage('Test') {
            steps {
                sh 'sh /var/lib/jenkins/test.sh'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'dev'
            }
            steps {
                sh './var/lib/jenkins/scripts/dev.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'bug'
            }
            steps {
                sh './var/lib/jenkins/scripts/bug.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
            }
        }
    }
}
