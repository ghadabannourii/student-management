pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
                sh 'echo "Build completed"'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
                sh 'echo "Tests executed"'
            }
        }

        stage('Run application') {
            steps {
                sh 'mvn spring-boot:run'
                sh 'echo "Application started"'
            }
        }

        stage('Archive artifact'){
            steps{
                archiveArtifacts artifacts: 'target/*.jar'
                fingerprint: true
            }
        }
    }
    post {
        failure {
            mail to:'ghadabannouri.221@gmail.com',
            subject : "Build Failed in Jenkins: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body : "Please go to ${env.BUILD_URL} to view the results."
        }
        success {
            mail to:'ghadabannouri.221@gmail.com',
            subject : "Build Success in Jenkins: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body : "Please go to ${env.BUILD_URL} to view the results."
        }
    }
}