pipeline {
    agent any
    tools {
        nodejs 'mohJ'
    } 
    stages {
        stage('Build') {
            steps {
                echo 'building your code'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests'
                sh 'npm test'
            }
        }
        stage('Sonar') {
            steps {
                echo 'Running Sonar'
                script {
                    def scannerHome = tool 'mohJ';
                    withSonarQubeEnv("MohSonarScanner") {
                        sh "${tool("mohJ")}/bin/sonar-scanner"
                    }
                }
            }
        }
    }
}
