pipeline {
    agent any
    parameters {
        string(name: 'version', defaultValue: '', description: 'artifact version')
    }
    stages {
        stage('init'){
            steps{
                script {
                   git branch: 'main', url: 'https://github.com/Achumbe/wordsmith-api.git'
                }
            }
        }
        stage('build'){
            tools{
                maven 'maven-3.9.3'
            }
            steps{
                script{
                    sh "mvn clean install -Dbuild.version=${params.version}"
                }
            }
        }
        stage('unit test'){
            tools{
                maven 'maven-3.9.3'
            }
            steps{
                script{
                    sh "mvn test"
                }
            }
        }
    }
}
