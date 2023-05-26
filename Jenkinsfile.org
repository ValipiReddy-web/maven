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
                sh 'sh /var/lib/jenkins/dev.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'bug'
            }
            steps {
                sh 'sh /var/lib/jenkins/bug.sh'
            }
        }
    }
}
