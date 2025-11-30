pipeline {
    agent any

    environment {
        IMAGE = "ghadabannourii/student"
        TAG = "latest"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE:$TAG .'
            }
        }

        stage('Docker Login & Push') {
            steps {
                withDockerRegistry([credentialsId: 'ghadabannourii-cred', url: 'https://index.docker.io/v1/']) {
                    sh 'docker push $IMAGE:$TAG'
                }
            }
        }
    }
}
