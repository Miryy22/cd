pipeline {
    agent any
    environment {
        DOCKER_HOST = 'tcp://PRODUCTION_SERVER_IP:2375' // Accès Docker distant
    }
    stages {
        stage('Checkout Code') {
            steps {
                // Récupérer le code source
                git branch: 'main', url: 'git@github.com:your-repo/project.git'
            }
        }
        stage('Build & Push Docker Images') {
            steps {
                script {
                    // Build et push des images Docker
                    sh 'docker-compose build'
                    sh 'docker-compose push'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    // Déploiement sur le serveur de production
                    sh 'ssh user@PRODUCTION_SERVER_IP "cd /path/to/project && docker-compose pull && docker-compose up -d"'
                }
            }
        }
    }
    triggers {
        // Déclenchement à chaque commit ou périodiquement
        scm('H/5 * * * *') // Poll Git toutes les 5 minutes
    }
}

