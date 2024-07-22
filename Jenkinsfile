pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/YOUR-GITHUB-ACCOUNT-NAME/SSDLAB7A_1.git', credentialsId: 'YOUR_CREDENTIALS_ID'
            }
        }
        stage('Build') {
            steps {
                sh 'docker pull composer:latest'
                sh 'docker run --rm composer:latest install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
