 
pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Initialize'){
            def dockerHome = tool 'myDocker'
            env.PATH = "${dockerHome}/bin:${env.PATH}"
        }
         stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }
        stage('Build') { 
            steps { 
                script{
                 app = docker.build("underwater")
                }
            }
        }
        stage('Test'){
            steps {
                 echo 'Empty'
            }
        }
        stage('Deploy') {
            steps {
                script{
                        docker.withRegistry('public.ecr.aws/c0l8l4b4/octopus-underwater-app', 'ecr:us-east-1:aws-credentials') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }
    }
}
