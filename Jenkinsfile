pipeline{
    agent any
    
    stages{
        stage("Code clone"){
            steps{
              echo "Cloning the code"
              git url:"https://github.com/himanshu8987/django-notes-app.git", branch: "main"
            }
            
        }
        stage("build"){
            steps{
                echo "Building the code"
                sh "docker build -t my-note-app ."
            }
            
        }
        stage("Push to Docker Hub"){
            steps{
               echo "Pushing the image to docker hub" 
               withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
               sh"docker tag my-note-app ${env.dockerhubUser}/my-note-app:latest"   
               sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
               sh "docker push ${env.dockerhubUser}/my-note-app:latest"
               }
            }
            
        }
        stage("Deploy"){
            steps{
               echo "Deploying the Container"
               sh "docker-compose down && docker-compose up -d"
            
            }
        }
    }
}
