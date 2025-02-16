pipeline {
    agent any

    environment {
        GITHUB_CREDENTIALS = 'github-token'  // Jenkins GitHub credentials
        MAVEN_TOOL = 'maven'  // Jenkins Maven tool name
        DOCKER_CREDENTIALS = 'docker-hub-credentials'  // Docker Hub credentials ID in Jenkins
        DOCKER_IMAGE = 'moinuddin62046/sample-java-app'  // Your Docker Hub repository
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/main']],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [],
                        userRemoteConfigs: [[
                            url: 'https://github.com/MOINUDDIN0786/my-java-app..git',
                            credentialsId: GITHUB_CREDENTIALS
                        ]]
                    ])
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    def mvnHome = tool name: MAVEN_TOOL, type: 'maven'
                    sh """
                        cd my-java-app
                        ${mvnHome}/bin/mvn clean package
                    """
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    def mvnHome = tool name: MAVEN_TOOL, type: 'maven'
                    sh """
                        cd my-java-app
                        ${mvnHome}/bin/mvn test
                    """
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh """
                        cd my-java-app
                        docker build -t ${DOCKER_IMAGE}:latest .
                    """
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    script {
                        sh """
                            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                            docker push ${DOCKER_IMAGE}:latest
                        """
                    }
                }
            }
        }
    }
}
