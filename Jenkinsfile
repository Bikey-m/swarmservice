pipeline {
    agent any
    
    environment {
        DOCKER_USERNAME = credentials('dockerhub-credentials')
        DOCKER_PASSWORD = credentials('dockerhub-credentials')
    }
    
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t $DOCKER_USERNAME/nginx .'
            }
        }
        
        stage('Push') {
            steps {
                sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                sh 'docker push $DOCKER_USERNAME/nginx'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
    
    post {
        always {
            node {
                sh 'docker logout'
            }
        }
    }
}
