@Library("Shared") _    // syntax of adding shared library. Shared is the name of the library
pipeline{
    
    agent {label "first"}
    
    stages{
        stage("Hello"){
            steps{
                script{
                    hello()  // name of groovy file(hello.groovy). calls this file from shared library
                }
            }
        }
        stage("Code"){
            steps{
                script{
                    clone("https://github.com/prajchi/django-notes-app.git", "main")
                }
            }
        }
        stage("Build"){
            steps{
                script{
                    docker_build("notes-app", "latest", "dockpra") // projectname, image name, username
                }
            }
        }
        stage("Push to Docker Hub"){
            steps{
                script{
                    docker_push("notes-app", "latest", "dockpra")
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "This is deploying the code"
                sh "docker compose up -d"
            }
        }
    }
}
