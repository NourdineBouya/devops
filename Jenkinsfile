pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "nourdinebouya/nextjs-app"
    }

    stages {
        stage('Build') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Push') {
            steps {
                script {
                    docker.withRegistry('', 'nourdinebouya') {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f k8s-deployment.yaml'
                }
            }
        }
    }
}
