pipeline {
    agent any
    stages {
        stage("Clone") {
            steps {
                git branch: "main", "https://github.com/bachlex03/jenkins.git"
            }
        }
    }
}