pipeline{
    stages{
        stage("Checkout Code Stage"){
            steps{
                git url:'https://github.com/rnvk/cicdpipe.git', branch:'main'
            }
        } 
        stage("Build docker images"){
            steps{
                sh 'docker build -t myimage16:latest1  . '
            }
        }
        stage("Push image to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:'dockerhub-credentials',
                usernameVariable:'DOCKER_USERNAME',passwordVariable:'DOCKER_PASSWORD')])
                {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker tag myimage16:latest1 $DOCKER_USERNAME/myimage16:latest1'
                    sh 'docker push $DOCKER_USERNAME/myimage16:latest1'
                }
            }
        }
        stage("kubernets deployment stage"){
            steps{
                sh 'kubectl apply -f  my-deployment.yml'
            }
        }
    }
}