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

        stage("Build Docker Image") {
            steps {
                sh "docker build -t javaapp ."
            }
        }

        stage("Tag & Push to DockerHub") {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker') {
                        sh "docker tag javaapp afeece/javaapp:latest"
                        sh "docker push afeece/javaapp:latest"
                    }
                }
            }
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
}