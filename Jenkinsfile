pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build and Push Docker Images') {
            steps {
                script {
                    echo "Building and pushing Docker images..."
                    def app1Image = docker.build("my-app1:${env.BUILD_ID}", "./app1")
                    app1Image.push()
            
                    def app2Image = docker.build("my-app2:${env.BUILD_ID}", "./app2")
                    app2Image.push()
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f k8s/deployment.yaml'
                }
            }
        }
    }
}
