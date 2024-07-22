pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/JIAJINSIM/SSDLAB7A_1.git', credentialsId: '113176322'
            }
        }
        stage('Build') {
            steps {
                // Ensure the correct directory is mounted
                sh 'docker pull composer:latest'
                sh 'docker run --rm -v $PWD:/app -w /app composer:latest install'
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
