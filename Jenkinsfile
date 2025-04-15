pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'python:3.11-slim'
                    reuseNode true
                }
            }
            steps {
                sh ''' 
                    python --version
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'python:3.11-slim'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    python3 app/main.py
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'This is where additional stages (such as Deploy) would go'
            }
        }
    }
}