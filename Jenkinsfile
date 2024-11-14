pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'ci-cd-demo-app'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/your-username/ci-cd-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'docker run $DOCKER_IMAGE'
                }
            }
        }

        stage('Deploy Application') {
            steps {
                script {
                    sh 'docker run -d -p 5000:5000 --name ci-cd-app $DOCKER_IMAGE'
                }
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
            slackSend(channel: '#ci-cd', color: 'good', message: "Build #${env.BUILD_NUMBER} succeeded!")
        }
        failure {
            echo 'Build failed!'
            slackSend(channel: '#ci-cd', color: 'danger', message: "Build #${env.BUILD_NUMBER} failed!")
        }
    }
}
