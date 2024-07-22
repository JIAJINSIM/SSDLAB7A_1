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
                // Run PHPUnit tests with docker-compose
                sh 'docker-compose run --rm composer ./vendor/bin/phpunit tests'
                // Run additional PHPUnit tests and generate JUnit report
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
