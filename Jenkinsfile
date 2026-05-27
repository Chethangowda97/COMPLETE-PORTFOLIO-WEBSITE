pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/Chethangowda97/COMPLETE-PORTFOLIO-WEBSITE.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t portfolio-website .'
            }
        }

        stage('Tag Docker Image') {
            steps {
                sh 'docker tag portfolio-website YOUR_DOCKERHUB_USERNAME/portfolio-website:v1'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'

                    sh 'docker push YOUR_DOCKERHUB_USERNAME/portfolio-website:v1'
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop portfolio-container || true
                docker rm portfolio-container || true

                docker run -d --name portfolio-container -p 80:80 \
                YOUR_DOCKERHUB_USERNAME/portfolio-website:v1
                '''
            }
        }
    }
}
