pipeline {
    agent {
        docker {
            image 'composer:latest'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/JIAJINSIM/SSDLAB7A_1.git', credentialsId: '113176322'
            }
        }
        stage('Adjust Permissions') {
            steps {
                // Adjust permissions to ensure Docker can write to the workspace directory
                sh 'chmod -R 777 $WORKSPACE'
            }
        }
        stage('Build') {
            steps {
                sh 'composer install'
            }
        }
        stage('Test') {
            steps {
                sh './vendor/bin/phpunit tests'
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
