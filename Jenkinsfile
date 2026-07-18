pipeline {
    agent any

    stages {

        stage('Verify Workspace') {
            steps {
                sh 'pwd'
                sh 'ls -la'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t divya-web:pipeline .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker rm -f divya-pipeline-container || true
                docker run -d --name divya-pipeline-container -p 8082:80 divya-web:pipeline
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }

        success {
            echo 'Application deployed successfully!'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}
