pipeline {
    agent any

    environment {
        DOCKERHUB = credentials('dockerhub-creds')
        HUB_USER  = oumaimabouhani
    }

    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Build images') {
            steps {
                sh 'docker build -t $HUB_USER/projets-backend:latest ./backend'
                sh 'docker build -t $HUB_USER/projets-frontend:latest ./frontend'
            }
        }
        stage('Login Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_PSW | docker login -u $DOCKERHUB_USR --password-stdin'
            }
        }
        stage('Push images') {
            steps {
                sh 'docker push $HUB_USER/projets-backend:latest'
                sh 'docker push $HUB_USER/projets-frontend:latest'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker compose down || true'
                sh 'docker compose up -d --build'
            }
        }
    }

    post {
        always { sh 'docker logout || true' }
    }
}
