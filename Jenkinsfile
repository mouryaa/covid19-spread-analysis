pipeline {
    environment {
        registry = "mouryaa/covid19-spread-analysis"
        registryCredential = 'dockerhub_id'
        dockerImage = ''
    }
    agent any

    stages {
        stage('Cloning our Git') {
            steps {
                git branch: 'main', url: 'https://github.com/mouryaa/covid19-spread-analysis.git'
            }
        }
        stage('Building our image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":latest"
                }
            }
        }
        stage('Deploy our image') {
            steps {
                script {
                    docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
