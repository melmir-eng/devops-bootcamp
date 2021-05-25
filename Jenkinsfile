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
        // stage('Sonar') {
        //     steps {
        //         echo 'Running Sonar'
        //         script {
        //             def scannerHome = tool 'mohJ';
        //             withSonarQubeEnv("MohSonar") {
        //                 sh "${tool("mohJ")}/bin/sonar-scanner"
        //             }
        //         }
        //     }
        // }
        stage('docker image build') {
            steps{
                withCredentials([usernamePassword(credentialsId: 'DockerRepo', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    sh '''
                        wget https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/docker-ce-cli_18.09.9~3-0~ubuntu-bionic_amd64.deb
                        dpkg -i ./docker-ce-cli_18.09.9~3-0~ubuntu-bionic_amd64.deb
                        apt-get update
                        apt-get install -y awscli
                        docker build -t workshopuser10:latest .
                        docker tag workshopuser10:latest workshopuser10:${BUILD_NUMBER}
                        docker tag workshopuser10:latest 686567993080.dkr.ecr.us-east-1.amazonaws.com/devopsbootcampuser10:latest
                        $(aws ecr get-login --region us-east-1 | sed 's/-e none//g')
                        docker push 686567993080.dkr.ecr.us-east-1.amazonaws.com/devopsbootcampuser10:latest
                    '''
}
            }
        }
    }
}
