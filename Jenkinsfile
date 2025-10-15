pipeline {
    agent any

    environment {
        NODEJS_HOME = tool name: 'NodeJS 18', type: 'NodeJS'
        PATH = "${env.NODEJS_HOME}\\bin;${env.PATH}"
        DEPLOY_DIR = 'C:\\hospital-frontend'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/suneethabulla/hospital-frontend.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Frontend') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                bat """
                if exist "${DEPLOY_DIR}\\*" rmdir /s /q "${DEPLOY_DIR}\\*"
                xcopy /E /I /Y dist\\* "${DEPLOY_DIR}\\"
                """
            }
        }
    }
}
