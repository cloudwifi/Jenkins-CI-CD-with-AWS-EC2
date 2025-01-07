pipeline {
    
    // Define the agent where the pipeline will run
    agent any 

    stages {
        stage("Cloning the code from a Git repository") {

            steps {

                // Clone the Git repository from the specified URL and branch
                git url: "https://github.com/cloudwifi/Jenkins-CI-CD-with-AWS-EC2.git", branch: "main"
                
                // Print a message in the console
                echo "Successfully cloned the code"

            }
        }

        stage("Building and testing the Docker image") {

            steps {
                // Build the Docker image 
                sh "docker build -t naveenjangid22/my-node-app . "

                // Print a message in the console
                echo "Successfully build the image"
            }
        }

        
        stage("Pushing to DockerHub") {

            steps {

                // Extract credentials for DockerHub stored in Jenkins
                withCredentials(
                    [usernamePassword(
                        credentialsId: "dockerhub_cred", // Jenkins credentials ID
                        usernameVariable: "naveenjangid22",
                        passwordVariable: "kota@1234#", 
                    )]
                )
                
                {
                    // Log in to DockerHub using the credentials
                    sh "docker login -u ${env.docker_hub_username} -p ${env.docker_hub_passsword}"
                    
                    // Print a message in the console
                    echo "Login to dockerhub sucess"

                    // Push the Docker image to DockerHub
                    sh "docker push naveenjangid22/my-node-app"

                    // Print a message in the console
                    echo "Succesfully pushed the image"

                }
            }
        }
        
        
        stage("Deploying the application using Docker Compose") {

            steps {
                // Bring up the Docker Compose services in detached mode
                sh "docker compose up -d"
            }

        }
    }
}
