pipeline {
    agent any

    environment {
        NODE_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
    }

    stages {
        stage('Checkout') {
            steps {
                node('master') { // Указываем label
                    git branch: 'main', url: 'https://github.com/burhon94/SPA.git'
                }
            }
        }
        stage('Install dependencies') {
            steps {
                node('master') {
                    sh 'npm install'
                }
            }
        }
        stage('Run tests') {
            steps {
                node('master') {
                    sh 'npm test'
                }
            }
        }
        stage('Build') {
            steps {
                node('master') {
                    sh 'npm run build'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
