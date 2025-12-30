pipeline {
    agent any

    options {
        timestamps()
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/YOUR_USERNAME/flask-ci-cd-demo.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh '''
                python -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh '''
                . venv/bin/activate
                pytest
                '''
            }
        }

        stage('Build Application') {
            steps {
                sh '''
                . venv/bin/activate
                python setup.py sdist
                '''
            }
        }

        stage('Simulate Deployment') {
            steps {
                sh '''
                mkdir -p /tmp/flask_deploy
                cp -r app /tmp/flask_deploy/
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
        always {
            cleanWs()
        }
    }
}
