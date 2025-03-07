pipeline{
    agent any
    stages{
        stage('CodeScan'){
            steps{
                sh 'trivy fs . -o file.txt'
                sh 'cat file.txt'

            }
        }
        stage('DockerBuild'){
            steps{
                sh 'docker build -t webapp .'
                sh 'docker images'

            }
        }
    }
}