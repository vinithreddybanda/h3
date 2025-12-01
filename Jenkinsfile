pipeline {
    agent any
    triggers {
        pollSCM('H/5 * * * *') // Polls every 5 minutes
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'No build steps required for HTML.'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Ready for deployment.'
            }
        }
    }
}