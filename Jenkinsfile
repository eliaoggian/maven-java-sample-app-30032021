pipeline {
    agent any

    stages {

        stage("Clean"){
            steps{
                sh "mvn clean"
            }
        }

        stage("Compile"){
            steps{
                sh "mvn compile"
            }
        }

        stage("Test"){
            steps{
                sh "mvn test"
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage("Sonar Scan"){
            steps{
                sh "mvn sonar:sonar -Dsonar.host.url=http://ec2-3-140-210-15.us-east-2.compute.amazonaws.com:9005 -Dsonar.login=0a0f3d64c353496711042451cfe566a3a972862c"
            }
        }

        stage("Package"){
            steps{
                sh "mvn package"
            }
            post {
                success {
                    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
            }
        }
    }
}