pipeline {
    agent any

    stages {
        stage('Install Docker') {
            steps {
                script {
                    // Update the package database
                    sh 'sudo apt-get update'
                    // Install required packages
                    sh 'sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common'
                    // Add Docker’s official GPG key
                    sh 'curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -'
                    // Add the Docker repository
                    sh 'sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"'
                    // Update the package database again
                    sh 'sudo apt-get update'
                    // Install Docker
                    sh 'sudo apt-get install -y docker-ce'
                    // Add the current user to the Docker group
                    sh 'sudo usermod -aG docker $USER'
                }
            }
        }

        stage('Install Docker Compose') {
            steps {
                script {
                    // Download the latest version of Docker Compose
                    sh 'sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose'
                    // Apply executable permissions to the binary
                    sh 'sudo chmod +x /usr/local/bin/docker-compose'
                    // Verify installation
                    sh 'docker-compose --version'
                }
            }
        }
    }

    post {
        always {
            // Clean up or notify if needed
            echo 'Docker and Docker Compose installation completed.'
        }
    }
}
