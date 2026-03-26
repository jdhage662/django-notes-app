@Library("Shared") _
pipeline{
    agent { label "jyoti"}
    stages{
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage("code"){
            steps{
                script{
                cloneProject("https://github.com/jdhage662/django-notes-app.git","main")
                }
            }
        }
        stage("build"){
             steps{
                    script{            
                    dockerbuild("notes-app","latest","jdhage")
                    }
                }

        }
        stage("push to docker hub"){
             steps{
                    echo "This is pushing the image to docker hub"
                    withCredentials([usernamePassword('credentialsId':"dockerHubCre",
                    'passwordVariable':"dockerHubCrePass",
                    'usernameVariable':"dockerHubCreUser")]){
                    sh "docker login -u ${env.dockerHubCreUser} -p ${env.dockerHubCrePass}"
                    sh "docker image tag notes-app:latest ${dockerHubCreUser}/notes-app:latest"
                    sh "docker push ${dockerHubCreUser}/notes-app:latest"
                    }
                }

        }
        stage("deploy"){
             steps{
                  echo "This is deploying the code"
                  echo "docker compose up -d"
                }
  
        }
    }
    
}
