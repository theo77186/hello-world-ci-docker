pipeline {
    environment {
        registry = "theo77186/helloworld"
        registryCredential = "docker-id"
        dockerImage = ""
    }
    agent any
    stages {
        stage("Git checkout") {
            steps {
                checkout scm
            }
        }

        stage("Building image") {
            steps {
                dir ("app") {
                    script {
                        dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    }
                }
            }
        }

        stage("Publish image") {
            steps {
                script {
                    docker.withRegistry("", registryCredential)
                    dockerImage.push()
                    dockerImage.push("latest")
                }
                echo "trying to push Docker Build to DockerHub"
            }
        }

        stage("Remove unused Docker image") {
            steps {
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}
