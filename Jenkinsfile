pipeline{
    agent any

    stages {
        stage('Cloning github repo to jenkins'){
            steps{
                script{
                    echo('Cloning ...')
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_token', url: 'https://github.com/AalokRawat/MLOPS-Project1.git']])
                }
            }
        }
    }
}