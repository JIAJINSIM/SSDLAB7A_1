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
                sh './vendor/bin/phpunit --log-junit logs/unitreport.xml -c tests/phpunit.xml tests'
            }
        }
        post {
			always {
				junit testResults: 'logs/unitreport.xml'
				}
        }
    }
}
