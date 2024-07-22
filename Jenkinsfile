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
                sh 'docker-compose run --rm composer'
            }
        }
        stage('Test') {
            steps {
                sh 'docker-compose run --rm composer ./vendor/bin/phpunit tests'
            }
        }
		}
}

