pipeline{
    agent any
    stages{
        stage('CodeScan'){
            steps{
                sh 'trivy fs . -o file.txt'
                sh 'cat file.txt'

            }
        }
        stage('DockerLogin'){
            steps{
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 954976287271.dkr.ecr.us-east-1.amazonaws.com'

            }
        }
        stage('DockerBuild'){
            steps{
                sh 'docker build -t githubpipeline .'
                sh 'docker images'
            }
        }
        stage('DockerImageTag'){
            steps{
                sh 'docker tag githubpipeline:latest 954976287271.dkr.ecr.us-east-1.amazonaws.com/githubpipeline:latest'
            }
        }
        stage('DockerPushImage'){
            steps{
                sh 'docker push 954976287271.dkr.ecr.us-east-1.amazonaws.com/githubpipeline:latest'
            }
        }
    }
}