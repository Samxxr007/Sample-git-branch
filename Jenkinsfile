pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'pytest'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t ex18-cicd-app:latest .'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker rm -f ex18-deployed || exit 0'
                bat 'docker run -d --name ex18-deployed -p 5000:5000 ex18-cicd-app:latest'
            }
        }
    }
}
