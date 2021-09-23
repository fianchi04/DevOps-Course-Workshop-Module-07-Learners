pipeline {
    agent none

    stages {
        stage('Build .NET') {
            
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
            agent {
                docker { image 'node:16-alpine' }
            }

            steps {
                echo 'Building Node..'
                dir ('DotnetTemplate.Web'){
                    sh 'npm install'
                    sh 'npm run build'
                    sh 'npm t'
                    sh 'npm run lint'
                }
                
            }
        }
    }
}