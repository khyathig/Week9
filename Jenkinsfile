
pipeline {
    agent any
    
    environment {
        PATH = "C:\\Users\\khyat\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin;${env.PATH}"
    }
   
    stages {
        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                bat "docker build -t kubedemoapp:v1 ."
            }
        }

        stage('Docker Login') {
            steps {
                bat 'docker login -u khyathig -p Docker@123'
            }
        }

        stage('push Docker Image to Docker Hub') {
            steps {
                echo "push Docker Image to Docker Hub"
                bat "docker tag kubedemoapp:v1 khyathig/sample:kubeimage1"

                bat "docker push khyathig/sample:kubeimage1"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                // apply deployment & service
                bat 'kubectl apply -f deployment.yaml --validate=false'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
