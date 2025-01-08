pipeline {
    agent any 

    stages {
        stage("Cloning the code from a Git repository") {
            steps {
                git url: "https://github.com/cloudwifi/Jenkins-CI-CD-with-AWS-EC2.git", branch: "main"
                echo "Successfully cloned the code"
            }
        }

        stage("Building and testing the Docker image") {
            steps {
                sh "docker build -t naveenjangid22/my-node-app . "
                echo "Successfully build the image"
            }
        }

        stage("Pushing to DockerHub") {
            steps {
                // Remove any previous Docker credentials
                sh "rm -rf ~/.docker/config.json"

                // Extract credentials for DockerHub stored in Jenkins
                withCredentials([usernamePassword(
                    credentialsId: "docker_credentials", 
                    usernameVariable: "docker_hub_username",
                    passwordVariable: "docker_hub_password"
                )]) {
                    echo "DockerHub Username: ${docker_hub_username}"
                    echo "DockerHub Password: ${docker_hub_password}"

                    // Log in to DockerHub using the credentials
                    sh "docker login -u ${docker_hub_username} -p ${docker_hub_password}"
                    echo "Login to DockerHub successful"

                    // Push the Docker image to DockerHub
                    sh "docker push naveenjangid22/my-node-app"
                    echo "Successfully pushed the image"
                }
            }
        }

        stage("Deploying the application using Docker Compose") {
            steps {
                sh "docker-compose up -d"
            }
        }
    }
}
