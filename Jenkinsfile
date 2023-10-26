pipeline {
    agent any 
    stages{
        stage("Code"){
            steps{
                echo "Cloning the code"
                git url : "https://github.com/Akshat0891/django-notes-app.git" , branch: "main"
            }
            
        }
        stage("Build"){
            steps{
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
            
        }
        stage("Push to DockerHub"){
            steps{
                echo "Logging and Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                    sh "docker tag my-note-app ${env.dockerhubUser}/mynote-app:latest"
                    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                    sh "docker push ${env.dockerhubUser}/mynote-app:latest"
                    
                }
            }
            
        }
        stage("Deploy"){
            steps{
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
            
        }
    }
}
