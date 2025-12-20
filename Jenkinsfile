pipeline{
    agent any

    environment {
        VENV_DIR = 'venv'
    }

    stages {
        stage('Cloning github repo to jenkins'){
            steps{
                script{
                    echo('Cloning github repo to jenkins')
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_token', url: 'https://github.com/AalokRawat/MLOPS-Project1.git']])
                }
            }
        }
    }

        stages {
        stage('Setting up our virtual env and installing dep'){
            steps{
                script{
                    echo('Setting up our virtual env and installing dep')
                    sh '''
                    python -m venv ${VEND_DIR}
                    . ${VEND_DIR}/bin/activate
                    pip install -upgrade pip
                    pip install -e .
                    '''
                }
            }
        }
    }
}