pipeline {
    agent any
    
    environment {
        DOCKER_USERNAME = credentials('bikeyaxxonet')
        DOCKER_PASSWORD = credentials('lifegood7775')
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
            sh 'docker logout'
        }
    }
}