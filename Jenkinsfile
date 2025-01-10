pipeline {
    agent any

    environment {
        NODE_VERSION = '16' // Задайте версию Node.js, подходящую для вашего проекта
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out repository...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Installing dependencies...'
                    // Настройка Node.js
                    sh '''
                    export NVM_DIR=$HOME/.nvm
                    . $NVM_DIR/nvm.sh
                    nvm install ${NODE_VERSION}
                    nvm use ${NODE_VERSION}
                    npm install
                    '''
                }
            }
        }

        stage('Build Project') {
            steps {
                script {
                    echo 'Building project...'
                    sh '''
                    export NVM_DIR=$HOME/.nvm
                    . $NVM_DIR/nvm.sh
                    nvm use ${NODE_VERSION}
                    npm run build
                    '''
                }
            }
        }

        stage('Post-Build Verification') {
            steps {
                echo 'Running post-build verification...'
                sh '''
                export NVM_DIR=$HOME/.nvm
                . $NVM_DIR/nvm.sh
                nvm use ${NODE_VERSION}
                npm run test
                '''
            }
        }

    }

    post {
        always {
            echo 'Cleaning up...'
            cleanWs() // Очищаем рабочую область после выполнения
        }
        success {
            echo 'Build successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
