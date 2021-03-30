pipeline {
    agent any

    stages {
        stage("Checkout"){
            steps{
                git "https://github.com/eliaoggian/maven-java-sample-app-30032021.git"
            }
        }

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
        }

        // stage("Scan"){

        // }

        stage("Package"){
            steps{
                sh "mvn package"
            }
        }

    }
    post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
        success{
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}