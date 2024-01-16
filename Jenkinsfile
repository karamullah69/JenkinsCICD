pipeline {
    agent {
        node {
            label 'docker-agent-alpine'
        }
    }    
    
    stages {
        stage('Build Hello World 1') {
            steps {
                script {
                    // Build Docker image for hello-world-1
                    dir('hello-world-1/src') {
                        sh 'docker build -t hello-world-1:latest .'
                    }
                }
            }
        }

        stage('Deploy Hello World 1') {
            steps {
                script {
                    // Deploy to Kubernetes for hello-world-1
                    kubernetesDeploy(
                        kubeconfigId: 'your-kubeconfig',
                        configs: 'hello-world-1/kube/deployment.yaml'
                    )
                }
            }
        }

        stage('Build Hello World 2') {
            steps {
                script {
                    // Build Docker image for hello-world-2
                    dir('hello-world-2/src') {
                        sh 'docker build -t hello-world-2:latest .'
                    }
                }
            }
        }

        stage('Deploy Hello World 2') {
            steps {
                script {
                    // Deploy to Kubernetes for hello-world-2
                    kubernetesDeploy(
                        kubeconfigId: 'your-kubeconfig',
                        configs: 'hello-world-2/kube/deployment.yaml'
                    )
                }
            }
        }
    }
}
