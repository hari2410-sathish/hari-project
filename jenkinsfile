pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo "Cloning repository..."
                // Jenkins already clones repo automatically in pipeline jobs
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image..."
                    docker.build('flask-demo-app')
                }
            }
        }

        stage('Run Container') {
            steps {
                echo "Running Docker container..."
                sh 'docker run -d -p 5000:5000 --name flask_app flask-demo-app || true'
            }
        }
    }

    post {
        always {
            echo "Cleaning up..."
            sh 'docker ps -a'
        }
    }
}
