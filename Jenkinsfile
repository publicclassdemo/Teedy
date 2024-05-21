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
                    docker.build('wikifor/teedy:latest') // Replace 'your-image-name:tag' with your desired image name and tag
                }
            }
        }
        // Pushing Docker image to Docker Hub
        stage('Upload image') {
            steps {
                script {
                    docker.withRegistry('', 'docker_hub') {
                        docker.image('wikifor/teedy:latest').push() // Replace 'your-image-name:tag' with your image name and tag
                    }
                }
            }
        }
        // Running Docker containers
        stage('Run containers') {
            steps {
                script {
                    docker.image('wikifor/teedy:latest').run('-p 8082:8080') // Replace 'your-image-name:tag' with your image name and tag
                    docker.image('wikifor/teedy:latest').run('-p 8083:8080') // Replace 'your-image-name:tag' with your image name and tag
                    docker.image('wikifor/teedy:latest').run('-p 8084:8080') // Replace 'your-image-name:tag' with your image name and tag
                }
            }
        }
    }
}
