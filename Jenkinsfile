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

        stage('Build') {
            steps {
                sh "mvn clean package -DskipTests"
            }
        }

        stage('SonarQube Analysis') {
            steps {
               withSonarQubeEnv(installationName: 'sq1') {
                    sh """
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=ghada \
                        -Dsonar.host.url=http://localhost:9000 \
                        -Dsonar.login=03dc318d1446a3f2cd763afb792334cb33a0b3bd
                    """
                }
            }
        }



       /* stage('Docker Build & Push') {
            steps {
                sh "docker build -t $IMAGE:$TAG ."
                withDockerRegistry([credentialsId: 'ghadabannourii', url: 'https://index.docker.io/v1/']) {
                    sh "docker push $IMAGE:$TAG"
                }
            }
        }*/
    }
}
