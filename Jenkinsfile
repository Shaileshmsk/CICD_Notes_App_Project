pipeline {
    agent any

    stages {
        stage('Code') {
            steps {
                echo 'Cloning the code'
                git url: "https://github.com/Shaileshmsk/CICD_Notes_App_Project.git", branch: "main"
            }
        }
        stage('Build'){
            steps {
                echo "Building the image"
                sh "docker build -t notes-app ."
            }
        }
        stage('Push to Docker Hub'){
            steps {
                echo "Pushing the image to Docker Hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag notes-app ${env.dockerHubUser}/notes-app:V1.0"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/notes-app:V1.0"
                }
            }
        }
        stage('Deploy'){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
