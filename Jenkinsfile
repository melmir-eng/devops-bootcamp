pipeline {
    agent any
    //tool name: 'mohJ', type: 'nodejs'
    tools {
        nodejs 'mohJ'
    } 
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                sh 'npm install'
            }
        }
    }
}
