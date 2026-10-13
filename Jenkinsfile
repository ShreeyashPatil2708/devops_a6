pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ShreeyashPatil2708/devops_a6.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'ls'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'python3 app.py'
            }
        }
    }
}
