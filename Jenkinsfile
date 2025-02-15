pipeline {
    agent any

    environment {
        GITHUB_CREDENTIALS = 'github-token'  // Update to your Jenkins SSH credentials ID
        MAVEN_TOOL = 'maven'  // Name of Maven tool configured in Jenkins
        SONARQUBE_SERVER = 'sonarqube'  // Update to your Jenkins SonarQube server ID
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
    }
}
