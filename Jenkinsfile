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
        
        stage('Check Docker') {
            steps {
                sh '''
                    whoami
                    pwd
                    which docker
                    docker --version
                '''
            }
        }

        stage("Build Docker Image") {
            steps {
                sh "docker build -t starbucks ."
            }
        }

        stage("Tag & Push to DockerHub") {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker') {
                        sh "docker tag starbucks vikas4cloud/starbucks:latest"
                        sh "docker push vikas4cloud/starbucks:latest"
                    }
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