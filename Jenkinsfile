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

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('MVN SONARQUBE') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'mvn clean verify sonar:sonar'
                }
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE:$TAG .'
            }
        }

        stage('Docker Login & Push') {
            steps {
                withDockerRegistry([credentialsId: 'ghadabannourii', url: 'https://index.docker.io/v1/']) {
                    sh 'docker push $IMAGE:$TAG'
                }
            }
        }
    }
}
