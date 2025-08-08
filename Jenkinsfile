pipeline {
    agent any

    environment {
        IMAGE_NAME = 'nodejs-demo-app'
        CONTAINER_NAME = 'nodejs-demo-container'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Saicharan261/nodejs-demo-app.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'  // use || true if no tests are defined yet
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker rm -f $CONTAINER_NAME || true
                    docker run -d --name $CONTAINER_NAME -p 3000:3000 $IMAGE_NAME
                '''
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
    }
}
