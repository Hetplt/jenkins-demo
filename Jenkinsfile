pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t het-cicd:v1 .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f het-cicd || true
                docker run -d --name het-cicd -p 8083:80 het-cicd:v1
                '''
            }
        }

        stage('Verify') {
            steps {
                sh 'curl localhost:8083'
            }
        }
    }
}
