@Library("shared") _
pipeline{
    agent { label "agent"}
    
  
    stages{
        
        stage("hello"){
            steps{
               script{
                   hello()
               } 
            }
        }
        
        stage("Code"){
            steps{
                script{
                clone( "https://github.com/saisuresh1209/django-notes-app.git","main")
                }
            }
        }
         stage("Build"){
            steps{
               script{
                   echo 'building code'
                   build("notes-app","latest","devsai1201")
               }
               
             

            }
        }
         stage("push to docker hub"){
            steps{
                withCredentials([usernamePassword('credentialsId':"dockerHubCred",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
                sh "docker push ${env.dockerHubUser}/notes-app:latest"
                }
            }
        }
         stage("Deploy"){
            steps{
                
                echo 'This is delopying the code'
                sh "docker compose up -d"
            }
        }
    }
}
