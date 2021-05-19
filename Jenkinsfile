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
    }
}
