pipeline{
    agent any
    options{
        timestamps()
    }
    stages{
        stage('Checkout Source'){
            steps{
                echo 'checking out code from git'
                git branch:'Main','url':'https://github.com/B-Kaushik21/python-jenkins-demo.git'
            }
        }
        stage('Install Dependencies'){
            steps{
                echo 'installing dependencies'
                bat 'pip install -r requirements.txt'
            }
        }
        stage('Build and Test'){
            steps{
                echo'running tests'
                bat 'pytest --junitxml=test-results.xml || exit 0'
            }
        }
        stage('Archive Test Reports'){
            steps{
                echo 'archiving test report'
                junit 'test-results.xml'
                archiveArtifacts artifacts: 'test-results.xml', fingerprint: true
            }
        }
    }
    post{
        success{
            echo 'pipeline completed successfully'
        }
        failure{
            echo 'pipelinie failed,check the logs'
        }
    }
}
