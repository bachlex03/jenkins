pipeline {
    environment {
        dockerHubCredentials = 'chani'
        dockerHubTag = "bale/chani-test"
        imageVersion = "v1"
    }


    agent any
    stages {
        stage("Clone") {
            steps {
                git branch: 'main', url: 'https://github.com/bachlex03/jenkins.git'
            }
        }

        stage("Deploy image") {
            steps {
                withDockerRegistry(credentialsId: "${dockerHubCredentials}", url: 'https://index.docker.io/v1/') {
                    sh label: 'build image', script: "docker build -t ${dockerHubTag}:${imageVersion} ."
                    sh label: 'push image', script: "docker push ${dockerHubTag}:${imageVersion}"
                }
            }
        }
    }
}