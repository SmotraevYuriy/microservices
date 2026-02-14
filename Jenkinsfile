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
                            bat 'mvn -q package'
                        }
                    }
                }
                stage('user-service') {
                    steps {
                        dir('userService') {
                            bat 'mvn -q package'
                        }
                    }
                }
                stage('orders-service') {
                    steps {
                        dir('ordersService') {
                            bat 'mvn -q package'
                        }
                    }
                }
            }
        }

        stage('Build Docker images') {
            steps {
                bat 'docker-compose build'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker-compose down'
                bat 'docker-compose up -d'
            }
        }
    }
}
