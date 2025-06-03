pipeline {
    agent { label 'debian' }

    environment {
        DEPLOY_DIR = '/home/curs/tender/wwwroot'
        GIT_REPO = 'https://github.com/deathMachine03/my-project.git'
        BRANCH = 'main'
    }

    stages {
        stage('Checkout') {
            steps {
                // Клонируем репозиторий с проектом
                git url: "${env.GIT_REPO}", branch: "${env.BRANCH}"
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React app') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Clean old files') {
            steps {
                sh "rm -rf ${DEPLOY_DIR}/*"
            }
        }

        stage('Deploy to server') {
            steps {
                sh "cp -r build/* ${DEPLOY_DIR}/"
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed.'
        }
    }
}
