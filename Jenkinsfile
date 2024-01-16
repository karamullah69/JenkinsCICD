pipeline {
    agent any
  
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
                    docker.build(DOCKER_IMAGE_NAME_1)
                    docker.withRegistry('https://index.docker.io/v1/', 'docker') {
                        docker.image(DOCKER_IMAGE_NAME_1).push()
                    }
                    docker.build(DOCKER_IMAGE_NAME_2)
                    docker.withRegistry('https://index.docker.io/v1/', 'docker') {
                        docker.image(DOCKER_IMAGE_NAME_2).push()
                    }
                    }
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    withCredentials([file(credentialsId: 'kube-config-credentials-id', variable: '4a8a395b-6461-49c3-a397-0746bc1d1348')]) {
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
