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
                sh 'docker build -t newversion .'
                sh 'docker images'
            }
        }
        stage('DockerImageTag'){
            steps{
                sh 'docker tag githubpipeline:latest 954976287271.dkr.ecr.us-east-1.amazonaws.com/githubpipeline:latest'
                sh 'docker tag githubpipeline:latest 954976287271.dkr.ecr.us-east-1.amazonaws.com/githubpipeline:v1.$BUILD_NUMBER'
            }
        }
        stage('DockerPushImage'){
            steps{
                sh 'docker push 954976287271.dkr.ecr.us-east-1.amazonaws.com/githubpipeline:latest'
                sh 'docker push 954976287271.dkr.ecr.us-east-1.amazonaws.com/githubpipeline:v1.$BUILD_NUMBER'
            }
        }
        stage('Testing'){
            steps{
                sh 'docker images'
                sh 'docker run -itd --name web -p 81:80 954976287271.dkr.ecr.us-east-1.amazonaws.com/'
            }
        }
    }
}