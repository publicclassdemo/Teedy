pipeline {
    agent any
    stages {
        stage('Package') {
            steps {
                checkout scm
                sh 'mvn -B -DskipTests clean package'
            }
        }
        // Building Docker image
        stage('Building image') {
            steps {
                script {
                    docker.build('kiritoharold/traccytian:latest') // Replace 'your-image-name:tag' with your desired image name and tag
                }
            }
        }
        // Pushing Docker image to Docker Hub
        stage('Upload image') {
            steps {
                script {
                    docker.withRegistry('', 'docker_hub') {
                        docker.image('kiritoharold/traccytian:latest').push() // Replace 'your-image-name:tag' with your image name and tag
                    }
                }
            }
        }
        // Running Docker containers
        stage('Run containers') {
            steps {
                script {
                    docker.image('kiritoharold/traccytian:latest').run('-p 10084:10084') // Replace 'your-image-name:tag' with your image name and tag
                    docker.image('kiritoharold/traccytian:latest').run('-p 10085:10085') // Replace 'your-image-name:tag' with your image name and tag
                    docker.image('kiritoharold/traccytian:latest').run('-p 10086:10086') // Replace 'your-image-name:tag' with your image name and tag
                }
            }
        }
    }
}
