pipeline {
    agent any

    environment {
        // Remplace 'dockerhub-credentials' par l'ID exact de ton credential Jenkins
        DOCKERHUB = credentials('dockerhub-credentials')
        HUB_USER  = 'oumaimabouhani'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build images') {
            steps {
                sh 'docker build -t $HUB_USER/projets-backend:latest ./backend'
                sh 'docker build -t $HUB_USER/projets-frontend:latest ./frontend'
            }
        }

        stage('Connexion Docker Hub') {
            steps {
                sh 'printf "%s" "$DOCKERHUB_PSW" | docker login -u "$DOCKERHUB_USR" --password-stdin'
            }
        }

        stage('Envoi images') {
            steps {
                sh 'docker push $HUB_USER/projets-backend:latest'
                sh 'docker push $HUB_USER/projets-frontend:latest'
            }
        }

        stage('Deploiement') {
            steps {
                // Remplace par ta commande de déploiement actuelle
                // (par exemple : docker compose up -d)
                sh 'echo "Deploiement a configurer"'
            }
        }
    }

    post {
        always {
            sh 'docker logout || true'
        }
    }
}
