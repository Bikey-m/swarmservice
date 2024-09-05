pipeline {
    agent any
    
    environment {
        DOCKER_USERNAME = credentials('khwairakpam.bm@axxonet.net') // Update with your Docker Hub credentials ID
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
            // Simplify to run sh without node or specify a label if needed
            sh 'docker logout'
        }
    }
}
