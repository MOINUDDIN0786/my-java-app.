pipeline {
    agent any

    environment {
        GITHUB_CREDENTIALS = 'github-pat'  // Make sure this matches the ID in Jenkins credentials
        MAVEN_TOOL = 'Maven'  // Ensure this is the correct Maven tool name in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            url: 'https://github.com/MOINUDDIN0786/my-java-app.git',
                            credentialsId: GITHUB_CREDENTIALS
                        ]]
                    ])
                }
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

