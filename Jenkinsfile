pipeline {
    agent any

    environment {
        NODE_VERSION = '16' // Задайте версию Node.js, подходящую для вашего проекта
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out repository...'
                git branch: 'master', url: 'https://github.com/burhon94/SPA.git'
            }
        }

        stage('Install Dependencies') {
			steps {
				echo 'Installing dependencies...'
				sh 'npm install'
			}
		}

		stage('Run Tests') {
			steps {
				echo 'Running tests...'
				sh 'npm test'
			}
		}

		stage('Build') {
			steps {
				echo 'Building project...'
				sh 'npm run build'
			}
		}

        stage('Deploy') {
            when {
                branch 'master' // Выполнять деплой только для основной ветки
            }
            steps {
                echo 'Deploying application...'
                sh '''
                # Пример деплоя: переместить файлы сборки в нужное место
                cp -R build/* /var/www/html/ # Убедитесь, что путь правильный для вашего сервера
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
