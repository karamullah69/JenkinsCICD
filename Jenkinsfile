pipeline {
    agent any
    
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('1dd069a1-4b2b-46e2-8cfb-3f61a21a77e0') // Create Jenkins credentials for Docker Hub
        KUBE_CONFIG = credentials('4a8a395b-6461-49c3-a397-0746bc1d1348') // Create Jenkins credentials for Kubernetes config file
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
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_HUB_CREDENTIALS) {
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
