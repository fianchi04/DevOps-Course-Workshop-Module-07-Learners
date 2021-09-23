pipeline {
    agent none

    stages {
        stage('Build .NET') {
            echo 'Building .Net...'
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk' }
            }
            environment {
                DOTNET_CLI_HOME = "/tmp/DOTNET_CLI_HOME"
            }
            steps {
                echo 'Building..'
                sh 'dotnet build'
                sh 'dotnet test'
            }
        }
        stage('Build Node') {
            echo 'Building Node...'
            agent {
                docker { image 'node:16-alpine' }
            }
            dir {
                path '/DotnetTemplate.Web'
            }
            
            steps {
                echo 'Building Node..'
                sh 'npm install'
                sh 'npm run build'
                sh 'npm t'
                sh 'npm run lint'
            }
        }
    }
}