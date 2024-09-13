pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the Git repository
                git url: 'https://github.com/atmanirbharcoder/Jenkins-Node-App-1.git', branch: 'master'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile in the repo
                    docker.build('Jenkins-Node-App-1:latest')
                }
            }
        }

        stage('Run Tests in Docker') {
            steps {
                script {
                    // Run the tests inside a container
                    docker.image('Jenkins-Node-App-1:latest').inside {
                        sh 'npm test'
                    }
                }
            }
        }

        stage('Build Application') {
            steps {
                script {
                    // Optionally build the application, e.g., for production
                    docker.image('Jenkins-Node-App-1:latest').inside {
                        sh 'npm run build'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // You can add your Docker deployment commands here
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished'
        }
        success {
            echo 'Build was successful'
        }
        failure {
            echo 'Build failed'
        }
    }
}
