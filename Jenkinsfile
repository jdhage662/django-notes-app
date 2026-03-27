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
                   script{
                       dockerpush("notes-app","latest")
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
