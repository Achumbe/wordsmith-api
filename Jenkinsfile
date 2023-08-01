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
        stage('sonar scan'){
            tools{
                maven 'maven-3.9.3'
            }
            steps{
               withSonarQubeEnv('sonar') {
                sh "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.1.2184:sonar -Dsonar.projectKey=frontend"
              }
            }
        }
        stage("Quality Gate"){
            steps{
                script{
                    timeout(time: 1, unit: 'HOURS') {
                    def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        error "Pipeline aborted due to quality gate failure: ${qg.status}"
                }
            }

                }
            }
          
        }
      
    }
}
