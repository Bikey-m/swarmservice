pipeline {
    agent any
    
    environment {
        DOCKER_USERNAME = credentials('khwairakpam.bm@axxonet.net')
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
            script {
                // Adding script block to ensure it's within a proper context
                try {
                    sh 'docker logout'
                } catch (e) {
                    echo "Logout failed: ${e.getMessage()}"
                }
            }
        }
    }
}
