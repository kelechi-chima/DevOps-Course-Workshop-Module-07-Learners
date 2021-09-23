pipeline {
    agent none
    stages {
        stage('Build dotnet artifacts') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk:5.0' }
            }
            environment {
                DOTNET_CLI_HOME = '/tmp/dotnet_cli_home'
            }
            steps {
                checkout scm
                sh 'dotnet build'
                sh 'dotnet test'
            }
        }
        stage('Build Typescript artifacts') {
            agent {
                docker { image 'node:16-alpine' }
            }
            steps {
                checkout scm
                dir('./DotnetTemplate.Web') {
                    sh 'npm install'
                    sh 'npm run build'
                    sh 'npm run lint'
                    sh 'npm t'
                }
            }
        }
    }
}