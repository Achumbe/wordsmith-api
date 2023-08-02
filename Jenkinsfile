pipeline {
    agent any

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
                maven "maven-3.9"
            }
            steps{
                script{
                sh "mvn clean install"
                }
            }
        }
        stage("Unit Test") {
            tools{
                maven "maven-3.9"
            }
            steps{
                script{
                sh "mvn test"
                }
            }
        }
    }
}