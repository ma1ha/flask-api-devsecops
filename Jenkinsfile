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
                sh 'docker build -t ${IMAGE_TAG} .'
            }
        }

       
        stage('Push to Docker Hub') {
            steps {steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: 'https://index.docker.io/v1/']) {
                    sh "docker push ${IMAGE_TAG}"  // Push the tagged image
                }
            }
        }
 
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
       
    }
}
