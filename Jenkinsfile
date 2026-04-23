pipeline {
agent any


environment {
    IMAGE_NAME = "praveenindevops/nodejs"
    IMAGE_TAG = "10.0.0"
    CONTAINER_NAME = "nodejs-container"
}

stages {

    stage('Checkout Code') {
        steps {
            git branch: 'main', url: 'https://github.com/praveenudemycourses/jenkins.git'
        }
    }

stage('Install & Test (Dockerized Node)') {
steps {
sh """
docker run --rm -v $PWD:/app -w /app node:18-alpine sh -c "npm install && npm test || true"
"""
}
}


    stage('Build Docker Image') {
        steps {
            sh 
            docker build -t $IMAGE_NAME:$IMAGE_TAG .
            
        }
    }

    stage('Run Container (Smoke Test)') {
        steps {
            sh 
            docker rm -f $CONTAINER_NAME || true
            docker run -d -p 3000:3000 --name $CONTAINER_NAME $IMAGE_NAME:$IMAGE_TAG
            sleep 10
            curl http://localhost:3000 || exit 1
            
        }
    }
}

post {
    always {
        sh 'docker system prune -f'
    }
}


}
