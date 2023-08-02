pipeline {
    agent any
    tools{
        maven "maven"
        jdk "jdk-17"
    }

    stages {
        stage("init") {
            steps{
                script{
                    git branch: 'main', url: 'https://github.com/Achumbe/wordsmith-api.git'
                }

            }
        }
        stage("Build Artifact") {
            steps{
                script{
                    sh "java --version"
                    sh "mvn clean install"
                }
            }
        }
        stage("Unit Test") {
            steps{
                script{
                sh "mvn test"
                }
            }
        }
    }
}