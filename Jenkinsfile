pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build services') {
            parallel {
                stage('gateway') {
                    steps {
                        dir('gateway') {
                            sh 'mvn -q package'
                        }
                    }
                }
                stage('user-service') {
                    steps {
                        dir('userService') {
                            sh 'mvn -q package'
                        }
                    }
                }
                stage('orders-service') {
                    steps {
                        dir('ordersSrvice') {
                            sh 'mvn -q package'
                        }
                    }
                }
            }
        }

        stage('Build Docker images') {
            steps {
                sh 'docker-compose build'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker-compose down'
                sh 'docker-compose up -d'
            }
        }
    }
}
