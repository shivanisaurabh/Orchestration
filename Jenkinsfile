pipeline {
agent any

```
environment {
    BACKEND_IMAGE = "shopnowbackend:1.0"
    FRONTEND_IMAGE = "shopnowfrontend:1.0"
    HELM_RELEASE = "shopnow"
    NAMESPACE = "default"
}

stages {

    stage('Checkout Code') {
        steps {
            git 'https://github.com/shivanisaurabh/Orchestration.git'
        }
    }

    stage('Build Backend Image') {
        steps {
            dir('backend') {
                sh 'docker build -t $BACKEND_IMAGE .'
            }
        }
    }

    stage('Build Frontend Image') {
        steps {
            dir('frontend') {
                sh 'docker build -t $FRONTEND_IMAGE .'
            }
        }
    }

    stage('Deploy to Kubernetes (Helm)') {
        steps {
            sh '''
            helm upgrade --install $HELM_RELEASE ./shopnow-chart \
            --set backend.image=$BACKEND_IMAGE \
            --set frontend.image=$FRONTEND_IMAGE
            '''
        }
    }

    stage('Verify Deployment') {
        steps {
            sh '''
            kubectl get pods
            kubectl get svc
            '''
        }
    }
}

post {
    success {
        echo '✅ CI/CD Pipeline executed successfully!'
    }
    failure {
        echo '❌ Pipeline failed. Check logs.'
    }
}
```

}
