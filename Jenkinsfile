pipeline {
    agent any

    environment {
        GITHUB_CREDENTIALS = 'github-token'  // Update to your Jenkins SSH credentials ID
        MAVEN_TOOL = 'Maven'  // Name of Maven tool configured in Jenkins
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
                            url: 'git@github.com:MOINUDDIN0786/my-java-app.git',
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
                    sh "${mvnHome}/bin/mvn clean package"
                }
            }
        }
    }
}
