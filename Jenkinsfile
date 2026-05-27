pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/Chethangowda97/COMPLETE-PORTFOLIO-WEBSITE.git'
            }
        }

        stage('Create Java File') {
            steps {
                sh '''
                echo 'public class App {
                    public static void main(String[] args) {
                        System.out.println("CI/CD Pipeline Success");
                    }
                }' > App.java
                '''
            }
        }

        stage('Build JAR') {
            steps {
                sh 'javac App.java'
                sh 'jar cvfe portfolio.jar App App.class'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t portfolio-image .'
            }
        }

    }
}
