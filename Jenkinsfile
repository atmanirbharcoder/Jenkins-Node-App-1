pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the Git repository
                git url: 'https://github.com/atmanirbharcoder/Jenkins-Node-App-1.git', branch: 'master'
            }
        }

        stage('Build Docker Image1.0') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile in the repo with sudo
                    sh 'sudo docker build -t Jenkins-Node-App-1:latest .'
                }
            }
        }


        stage('Build Docker Image1.1') {
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
                        sh 'npm install'  // Ensure dependencies are installed before running tests
                        sh 'npm test'     // Run tests
                    }
                }
            }
        }

        stage('Build Application') {
            steps {
                script {
                    // Build the application, e.g., for production
                    docker.image('Jenkins-Node-App-1:latest').inside {
                        sh 'npm run build'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Add Docker deployment commands, e.g., pushing to a registry or starting a container
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
