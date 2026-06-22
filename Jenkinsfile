pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning the repository...'
                git branch: 'main', url: 'https://github.com/umeshbharude929/simple-java-docker.git'
            }
        }
        
        stage('Compile Java Code') {
            steps {
                echo 'Compiling Java code...'
                sh 'javac src/Main.java'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
                sh 'docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${IMAGE_NAME}:latest'
            }
        }
        
        // stage('Run Docker Container') {
        //     steps {
        //         echo 'Running Docker container...'
        //         sh '''
        //             docker run --rm ${IMAGE_NAME}:${IMAGE_TAG}
        //         '''
        //     }
        // }
    }
    
    post {
        always {
            echo 'Pipeline completed'
        }
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed. Please check the logs above.'
        }
    }
}