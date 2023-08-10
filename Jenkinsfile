pipeline {
    agent any
    tools {
        maven "maven"
    }
    stages {
        stage("init"){
            steps{
                script {
                    git branch: 'main', url: 'https://github.com/Achumbe/wordsmith-api.git'
                }
            }
        }
        stage("version") {
            steps{
                script{
                   getDockerTag() 
                }
            }
        }
        // stage("Build Artifact") {
        //     tools {
        //         jdk "jdk"
        //     }
        //     steps {
        //         script {
        //             sh "java --version"
        //             sh "mvn clean install"
        //         }
        //     }
        // }
        // stage("Unit Test") {
        //     steps {
        //         script {
        //             sh "mvn test"
        //         }
        //     }
        // }
        // stage('Sonar Scan') {
        //     steps {
        //         withSonarQubeEnv("sonar"){
        //             sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
        //         }
        //     }
        // }
        // stage("Quality Gate"){
        //     steps{
        //         script{
        //             timeout(time: 1, unit: 'HOURS') { 
        //                 def qg = waitForQualityGate() 
        //                 if (qg.status != 'OK') {
        //                     error "Pipeline aborted due to quality gate failure: ${qg.status}"
        //                 }
        //             }
        //         }
        //     }
        // }
        // stage ("Build Docker Image") {
        //     steps {
        //         script {
        //             sh "docker build -t 602182454152.dkr.ecr.us-east-1.amazonaws.com/wordsmith-api:1.1.0-SNAPSHOT ."
        //         }
        //     }
        // }

        // stage("Push to ECR"){
        //     steps {
        //         script{
        //             withAWS([credentials: 'aws-creds', region: 'us-east-2']) {
        //                 sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 602182454152.dkr.ecr.us-east-1.amazonaws.com"
        //                 sh "docker push 602182454152.dkr.ecr.us-east-1.amazonaws.com/wordsmith-api:1.1.0-SNAPSHOT"
        //             }
        //         }
        //     }
        // }
    }
}

def getDockerTag() {
    //develope=> 1.1.0.230-rc | master => 1.1.0.200 | feature => 1.1.0.240-feature-something
    def pom = readMavenPom(file: 'pom.xml')
    def version = pom.version
    def branch = "${env.BRANCH_NAME}"
    def build_number = "${env.BUILD_NUMBER}"

    def tag = ""
    
    if (branch == 'main'){
        tag = "${version}.${build_number}"
    } else if(branch == "develop"){
        tag = "${version}.${build_number}-rc"
    } else {
        branch = branch.replace("/", "-").replace("\\", "-")
        tag = "${version}-${branch}.${build_number}"
    }
    
    println tag
    return tag

}
