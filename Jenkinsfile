pipeline {
    environment {
        dockerHubCredentials = 'chani'
        dockerHubTag = "baledev/chani-test"
        imageVersion = "v1"
    }


    agent any
    stages {
        stage("Clone") {
            steps {
                git branch: 'main', url: 'https://github.com/bachlex03/jenkins.git'
            }
        }

        stage("Deploy images to Docker Hub") {
            steps {
                withDockerRegistry(credentialsId: "${dockerHubCredentials}", url: 'https://index.docker.io/v1/') {
                    // sh "docker ps -a"
                    // sh label: 'build image', script: "docker build -t ${dockerHubTag}:${imageVersion} ."
                    // sh label: 'push image', script: "docker push ${dockerHubTag}:${imageVersion}"

                    sh label: "build images", script: "docker compose build"
                    sh label: "push images", script: "docker compose push"
                }
            }
        }

        stage ("Deploy to DEV environment") {
            steps {
                echo "Deploying to DEV environment"
                sh "docker compose down -v"
                sh "echo y | docker container prune -f"
                
                sh "docker compose up -d"

                sh "docker ps -a"
            }
        }
    }
}