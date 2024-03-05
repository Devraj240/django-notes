pipeline {
    agent any
    
    stages{
        stage("GIT CLONE CODE"){
            steps{
                echo "Cloning the code"
                git url:"https://github.com/Devraj240/django-notes.git", branch:"main"
            }
        }
        stage("BUILD"){
            steps{
                echo " Building the image "
                sh " docker build -t my-note-app . "
            }
            
        }
        stage("PUSH TO DOCKER HUB"){
            steps{
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPass', usernameVariable: 'deraooo')]){
                sh "docker tag my-note-app ${env.deraooo}/my-note-app:latest"
                sh "docker login -u ${env.deraooo} -p ${env.dockerHubPass}"
                sh "docker push ${env.deraooo}/my-note-app:latest"
                 }
            }
        }
        stage("DEPLOY"){
            steps{
                echo "Deploying the contianer and removing old container "
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPass', usernameVariable: 'deraooo')]){
                sh "docker run -d -p 8000:8000 ${env.deraooo}/my-note-app:latest"
}
            }
            
        }
        
    }
