pipeline {
    agent any

    environment {
        IMAGE = "ghadabannourii/student-Management"
        TAG = "latest"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

       stage('Docker login') {
                   steps {
                       withDockerRegistry([
                           credentialsId: 'ghadabannourii',
                           url: 'https://index.docker.io/v1/'
                       ]) {
                           sh 'echo docker login successful'
                           sh "docker push ${DOCKER_IMAGE}"
                           sh 'echo "docker push successful"'
                       }
                   }
               }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE:$TAG .'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $IMAGE:$TAG'
            }
        }
    }
}