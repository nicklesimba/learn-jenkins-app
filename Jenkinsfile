pipeline {
    agent any

    // environment {
    //     // Optional: you can inject credentials here if needed
    //     // GITHUB_TOKEN = credentials('github-pat')
    // }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                script {
                    githubNotify context: 'Build', description: 'Starting build...', status: 'PENDING'
                }
                sh ''' 
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
            post {
                success {
                    script {
                        githubNotify context: 'Build', description: 'Build successful', status: 'SUCCESS'
                    }
                }
                failure {
                    script {
                        githubNotify context: 'Build', description: 'Build failed', status: 'FAILURE'
                    }
                }
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                script {
                    githubNotify context: 'Test', description: 'Running tests...', status: 'PENDING'
                }

                sh '''
                    test -f build/index.html
                '''
            }
            post {
                success {
                    script {
                        githubNotify context: 'Test', description: 'Tests passed', status: 'SUCCESS'
                    }
                }
                failure {
                    script {
                        githubNotify context: 'Test', description: 'Tests failed', status: 'FAILURE'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}