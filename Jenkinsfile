pipeline {
    agent any
    tools{
        maven "maven"
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
            tools{
                jdk "jdk-17"
            }
            steps{
                script{
                    sh "ls -l"
                    sh "mvn clean install"
                    sh "java --version"
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