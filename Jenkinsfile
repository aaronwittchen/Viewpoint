pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
        DOCKERHUB_USER = 'onionn'
        FRONTEND_IMAGE = 'onionn/viewpoint-frontend'
        BACKEND_IMAGE = 'onionn/viewpoint-backend'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Images') {
            parallel {
                stage('Build Frontend') {
                    steps {
                        dir('frontend') {
                            sh 'docker build -t $FRONTEND_IMAGE:$BUILD_NUMBER -t $FRONTEND_IMAGE:latest .'
                        }
                    }
                }
                stage('Build Backend') {
                    steps {
                        dir('backend') {
                            sh 'docker build -t $BACKEND_IMAGE:$BUILD_NUMBER -t $BACKEND_IMAGE:latest .'
                        }
                    }
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push Images') {
            parallel {
                stage('Push Frontend') {
                    steps {
                        sh 'docker push $FRONTEND_IMAGE:$BUILD_NUMBER'
                        sh 'docker push $FRONTEND_IMAGE:latest'
                    }
                }
                stage('Push Backend') {
                    steps {
                        sh 'docker push $BACKEND_IMAGE:$BUILD_NUMBER'
                        sh 'docker push $BACKEND_IMAGE:latest'
                    }
                }
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
