pipeline {
    triggers {
        githubPush() // only trigger on GitHub push
    }

    agent {
        docker {
            image 'python:3.10'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install --upgrade pip'
                sh './venv/bin/pip install -r requirements.txt'
                sh './venv/bin/pip install pytest'
            }
        }

        stage('Run tests') {
            steps {
                sh './venv/bin/pytest'
            }
        }
    }

    post {
        always {
            junit '**/test-results.xml' // Optional: if you're capturing results
        }
        success {
            echo 'Tests passed!'
        }
        failure {
            echo 'Tests failed.'
        }
    }
}


