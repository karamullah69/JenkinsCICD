pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build and Deploy Hello World 1') {
            steps {
                script {
                    // Build Docker image for hello-world-1
                    dir('hello-world-1/src') {
                        sh 'docker build -t hello-world-1:latest .'
                    }

                    // Deploy to Kubernetes for hello-world-1
                    kubernetesDeploy(
                        kubeconfigId: 'your-kubeconfig',
                        configs: 'hello-world-1/deployment.yaml'
                    )
                }
            }
        }

        stage('Build and Deploy Hello World 2') {
            steps {
                script {
                    // Build Docker image for hello-world-2
                    dir('hello-world-2/src') {
                        sh 'docker build -t hello-world-2:latest .'
                    }

                    // Deploy to Kubernetes for hello-world-2
                    kubernetesDeploy(
                        kubeconfigId: 'your-kubeconfig',
                        configs: 'hello-world-2/deployment.yaml'
                    )
                }
            }
        }
    }
}
