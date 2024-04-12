pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/AKs1190/Microservice.git'
            }
        }
        stage('Trivy FS scan') {
           steps {
                 
                 sh "trivy fs --format table -o trivy-fs-report.html ."
            }
        }
         stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t aks1105/adservice:V1 ."
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push aks1105/adservice:V1 "
                    }
                }
            }
        }
    }
}
