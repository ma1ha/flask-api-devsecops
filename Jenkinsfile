pipeline {
    agent any 

    environment {
        IMAGE_NAME = "maha997/flask-api"
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
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
/*
        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push $IMAGE_NAME'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }*/
         stage('Docker Build') {
      agent any
      steps {
        sh 'docker build $IMAGE_NAME .'
      }
    }
}
