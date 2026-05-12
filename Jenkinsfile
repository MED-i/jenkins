pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def branch = env.GIT_BRANCH
                    def port = (branch == 'origin/main') ? 3000 : 3001
                    sh "docker build -t myapp:${branch} ."
                    sh "docker run -d -p ${port}:${port} myapp:${branch}"
                }
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying branch ${env.GIT_BRANCH}"
            }
        }
    }
}
