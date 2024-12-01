pipeline {
    agent any

    environment {
        DOCKER = 'docker'
        DOCKER_CREDENTIALS = credentials('secret-test')
    }

    stages {
        
         stage('Build') {
             agent {
                 docker {
                    image 'node:18-alpine'
                    reuseNode true
                 }
             }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'npm test'
                echo '$DOCKER'
                echo '$DOCKER_CREDENTIALS'
            }
        }
    }

    // post {
    //     always {
    //         junit 'test-results/junit.xml'
    //     }
    // }
}
