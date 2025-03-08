pipeline{
    agent any 
    enviroment{
        IMAGE_NAME="maha997/flask-api"

    }
    stages{
        stage('checkout code'){
            steps{ 
                git "https://github.com/ma1ha/flask-api.git"
            }
        }
        stage('Build Docker Images'){
            sh 'docker build -t $IMAGE_NAME .'
        }
        stage(' Push to docker hub'){
            withDockerRegistry([ credentialsId: ' docker-hub-credentials', url: '']){
                sh 'docker push $IMAGE_NAME'

            }
            stage(' Deploy to kubernetes'){
                steps{
                    sh 'kubectl apply -f k8s/deployment.yaml'
                }
            }
        }
    }
}