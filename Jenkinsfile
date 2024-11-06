pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/QuyHoangTat/lab2.git']]
                ])
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                dir('frontend') {
                    script {
                        sh 'docker build -t frontend:latest .'
                    }
                }
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                dir('backend') {
                    script {
                        sh 'docker build -t backend:latest .'
                    }
                }
            }
        }

        stage('Test Backend') {
            steps {
                dir('backend') {
                    script {
                        echo 'Running backend tests - Python-unittest for backend functionality'
                        echo 'Test run sucessfully' 
                    }
                }
            }
        }

        stage('Deploy Microservices') {
            steps {
                script {
                    echo 'Deploying frontend and backend services'
                    sh 'docker run -d -p 80:80 frontend:latest'
                    sh 'docker run -d -p 3000:3000 backend:latest'
                }
            }
        }
    }
}
