pipeline {
    agent any

    options {
        timestamps()
    }

    stages {

        stage('Install Dependencies') {
            steps {
                bat '''
                python -m venv venv
                call venv\\Scripts\\activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat '''
                call venv\\Scripts\\activate
                pytest
                '''
            }
        }

        stage('Build Application') {
            steps {
                bat '''
                if not exist build mkdir build
                xcopy app build\\app /E /I /Y
                '''
            }
        }

        stage('Simulate Deployment') {
            steps {
                bat '''
                if not exist C:\\tmp\\ssd_deploy mkdir C:\\tmp\\ssd_deploy
                xcopy build C:\\tmp\\ssd_deploy /E /I /Y
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
        always {
            cleanWs()
        }
    }
}
