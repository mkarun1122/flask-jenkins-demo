pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/<your-username>/flask-jenkins-demo.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'python -m unittest discover'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Starting Flask App...'
                bat 'python app.py'
            }
        }
    }
}
