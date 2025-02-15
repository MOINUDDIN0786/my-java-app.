pipeline {
    agent any

    environment {
        GITHUB_CREDENTIALS = 'github-ssh'  // Update to your Jenkins SSH credentials ID
        MAVEN_TOOL = 'Maven'  // Name of Maven tool configured in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    credentialsId: GITHUB_CREDENTIALS,
                    url: 'git@github.com:MOINUDDIN0786/my-java-app.git'  // Use SSH URL
            }
        }

        stage('Build') {
            steps {
                script {
                    def mvnHome = tool MAVEN_TOOL
                    sh "${mvnHome}/bin/mvn clean package"
                }
            }
        }
    }
}
