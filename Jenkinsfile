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

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''
                        mvn clean verify sonar:sonar \
                        -sonar.projectKey=ghada \
                        -sonar.host.url=http://localhost:9000 \
                        -sonar.login=03dc318d1446a3f2cd763afb792334cb33a0b3bd
                    '''
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
