pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    echo "🛠 Building Docker image..."
                    docker.build('hari-project-1')
                }
            }
        }

        stage('Clean Old Container') {
            steps {
                echo "🧹 Removing old container (if exists)..."
                sh 'docker rm -f hari || true'
            }
        }

        stage('Run Container') {
            steps {
                echo "🚀 Running container..."
                sh '''
                    docker run -d -p 500:5000 --name hari hari-project
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
