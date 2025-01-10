pipeline {
    agent any

    environment {
        NODE_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
    }

    stages {
        stage('Checkout') {
            steps {
                node {
                    git branch: 'main', url: 'https://github.com/your-username/your-repo.git'
                }
            }
        }
        stage('Install dependencies') {
            steps {
                node {
                    sh 'npm install'
                }
            }
        }
        stage('Run tests') {
            steps {
                node {
                    sh 'npm test'
                }
            }
        }
        stage('Build') {
            steps {
                node {
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
