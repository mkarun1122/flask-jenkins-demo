pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/mkarun1122/flask-jenkins-demo.git'
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
