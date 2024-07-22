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
        stage('Test1') {
            steps {
                sh 'docker-compose run --rm composer ./vendor/bin/phpunit tests'
            }
        }
        stage('Test2') {
            steps {
                sh 'docker-compose run --rm composer ./vendor/bin/phpunit --log-junit logs/unitreport.xml -c tests/phpunit.xml tests'
            }
        }
    }
    post {
        always {
            // Publish JUnit test results
            junit testResults: 'logs/unitreport.xml'
        }
    }
}
