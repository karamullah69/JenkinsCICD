pipeline {
    agent any
    
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-registry-credentials') // Create Jenkins credentials for Docker Hub
        KUBE_CONFIG = credentials('your-kubeconfig') // Create Jenkins credentials for Kubernetes config file
    }
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }
        
        stage('Build and Push Docker Images') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                        // Build and push Hello World 1 image
                        def dockerImage1 = docker.build("karamullah69/hello-world-1:latest", "-f Dockerfile1 .")
                        dockerImage1.push()

                        // Build and push Hello World 2 image
                        def dockerImage2 = docker.build("karamullah69/hello-world-2:latest", "-f Dockerfile2 .")
                        dockerImage2.push()
                    }
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    withCredentials([file(credentialsId: 'kube-config-credentials-id', variable: 'KUBE_CONFIG')]) {
                        sh """
                            kubectl --kubeconfig=\$KUBE_CONFIG apply -f k8s/deployment.yaml
                            kubectl --kubeconfig=\$KUBE_CONFIG apply -f k8s/service.yaml
                        """
                    }
                }
            }
        }
    }
}
