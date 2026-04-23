pipeline {
agent any

```
environment {
    IMAGE_NAME = "praveenindevops/nodejs"
    IMAGE_TAG = "10.0.0"
    CONTAINER_NAME = "nodejs-container"
}

stages {

    stage('Checkout Code') {
        steps {
            git url: 'https://github.com/praveenudemycourses/jenkins.git', branch: 'main'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
        }
    }

    stage('Run Container') {
        steps {
            sh "docker rm -f ${CONTAINER_NAME} || true"
            sh "docker run -d -p 3000:3000 --name ${CONTAINER_NAME} ${IMAGE_NAME}:${IMAGE_TAG}"
        }
    }

}

post {
    always {
        sh "docker system prune -f"
    }
}
```

}
