pipeline {
    agent any 

    environment {
        IMAGE_NAME = "maha997/flask-api"
        IMAGE_TAG = "${IMAGE_NAME}:${BUILD_NUMBER}" 
    }

    stages {
        stage('Checkout Code') {
            steps { 
                git branch: 'main', 
                    credentialsId: 'github-credentials', 
                    url: "https://github.com/ma1ha/flask-api-devsecops.git"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_TAG} ."  // Proper string interpolation
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: 'https://index.docker.io/v1/']) {
                    sh "docker push ${IMAGE_TAG}"
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG')]) {
                    
                    export PATH=${KUBECTL_PATH}:$PATH
                    kubectl version --client
                    kubectl cluster-info
                    kubectl get nodes
                    kubectl apply -f k8s/pingpong.yaml

                '''
            }
        }
    }
} 
