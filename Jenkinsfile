pipeline {
    agent any

    stages {

        stage('Build Backend Image') {
            steps {
                dir('backend') {
                    sh 'docker build -t shopnow-backend .'
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                dir('frontend') {
                    sh 'docker build -t shopnow-frontend .'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }
    }
}