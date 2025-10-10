pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    echo "🛠 Building Docker image..."
                    docker.build('flask-demo-app')
                }
            }
        }

        stage('Clean Old Container') {
            steps {
                echo "🧹 Removing old container (if exists)..."
                sh 'docker rm -f flask_app || true'
            }
        }

        stage('Run Container') {
            steps {
                echo "🚀 Running container..."
                sh '''
                    docker run -d -p 5000:5000 --name flask_app flask-demo-app
                    docker ps -a
                '''
            }
        }
    }

    post {
        always {
            echo "📦 Post-build: show containers"
            sh 'docker ps -a'
        }
    }
}
