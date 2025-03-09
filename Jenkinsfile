pipeline{
    agent {label 'ubuntu-agent'}
    stages{
        stage('TestingUbuntu'){
            steps{
                sh 'python3 --version'
                sh 'docker --version'
                sh 'java --version'
            }
        }
    }
}