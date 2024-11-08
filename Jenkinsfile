pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/riddhish143/Electronic-Mart.git'
        DOCKER_COMPOSE_FILE = 'docker-compose.yaml'
        GITHUB_CREDENTIALS = credentials('github-pat') // Reference the stored credential
        AWS_PUBLIC_IP = '13.200.200.254' // Replace with your actual AWS instance public IP
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub using the PAT
                git url: "${REPO_URL}", branch: 'main', credentialsId: 'github-pat'
            }
        }

        stage('Build Docker Images') {
            steps {
                // Build Docker images for the services
                script {
                    sh 'docker-compose -f ${DOCKER_COMPOSE_FILE} build'
                }
            }
        }

        stage('Run Docker Compose') {
            steps {
                // Run the Docker Compose to start the services
                script {
                    sh 'docker-compose -f ${DOCKER_COMPOSE_FILE} up -d'
                }
            }
        }

        stage('Curl Website') {
            steps {
                // Curl the website using the AWS instance public IP
                script {
                    sh "curl http://${AWS_PUBLIC_IP}" // Make sure the service is running on the expected port
                }
            }
        }

        // stage('Clean Up') {
        //     steps {
        //         // Clean up the Docker environment
        //         script {
        //             sh 'docker-compose -f ${DOCKER_COMPOSE_FILE} down'
        //         }
        //     }
        // }
    }

    post {
        always {
            // Archive the logs or any artifacts if needed
            archiveArtifacts artifacts: '/logs/*', allowEmptyArchive: true
        }
    }
}