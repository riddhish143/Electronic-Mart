pipeline {
    agent any

    stages {
        stage('Install Docker and Docker Compose') {
            steps {
                script {
                    // Run the installation script with the full path
                    sh 'sudo /root/install.sh'
                }
            }
        }
    }

    post {
        always {
            echo 'Docker and Docker Compose installation completed.'
        }
    }
}