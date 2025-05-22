pipeline {
    agent any

    environment {
        IMAGE_NAME = "hello-python-app"
        SONARQUBE_ENV = "SonarQubeServer" // Replace with your SonarQube server name in Jenkins
    }

    stages {
        stage('Clone GitHub Repo') {
            steps {
                echo 'Cloning the GitHub repository...'
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                echo 'Running SonarQube analysis...'
                withSonarQubeEnv("${SONARQUBE_ENV}") {
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image locally...'
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container...'
                sh "docker run --rm $IMAGE_NAME"
            }
        }
    }
}
