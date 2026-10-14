pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ShreeyashPatil2708/devops_a6.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'python3 app.py'
                // On Windows agents, use: bat 'python app.py'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'python3 -m py_compile app.py'
                // On Windows agents, use: bat 'python -m py_compile app.py'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the console output above for errors.'
        }
    }
}
