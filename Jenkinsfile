pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build('flask-mysql-crud-app')
                }
            }
        }
        stage('Test') {
            steps {
                sh 'python -m unittest discover -s tests'
            }
        }
        stage('Push to Registry') {
            steps {
                script {
                    docker.withRegistry('https://your-docker-registry.com', 'docker-credentials-id') {
                        docker.image('flask-mysql-crud-app').push('latest')
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }
    }
}
