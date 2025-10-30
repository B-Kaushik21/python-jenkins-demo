pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Python dependencies...'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Build') {
            steps {
                echo 'Running main Python app...'
                sh 'python app.py'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'pytest test_app.py --maxfail=1 --disable-warnings -q'
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo 'Archiving build outputs...'
                archiveArtifacts artifacts: '**/*.py', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build completed successfully!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
