pipeline {
    agent {
        node {
            label 'docker-my'
        }
    }

    stages {
        stage('Check Docker') {
            steps {
                script {
                    // Add Docker to PATH
                    def dockerPath = tool 'Docker'
                    env.PATH = "${dockerPath}:${env.PATH}"

                    // Verify Docker installation
                    sh 'docker --version'
                }
            }
        }
        
        stage('Build Hello World 1') {
            steps {
                script {
                    // Add Docker to PATH
                    def dockerPath = tool 'Docker'
                    env.PATH = "${dockerPath}:${env.PATH}"
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
                        configs: 'deployment1.yaml'
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
                        configs: 'deployment2.yaml'
                    )
                }
            }
        }
    }
}
