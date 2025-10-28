pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/<your-username>/jenkins-python-poc.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest > result.log || true'
                sh 'cat result.log'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-python-poc .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 5000:5000 jenkins-python-poc'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'docker ps -a'
        }
    }
}
