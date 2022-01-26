pipeline {
    agent any

    stages {
        stage('Clean workspace') {
            steps {
                cleanWs()
            }
        }
        
        stage ('Git Checkout') {
            steps {
                git branch: 'master', credentialsId: 'trungtin1209', url: 'https://github.com/trungtin1209/OktaJenkinsCI.git'
            }
        }
        
        stage('Restore packages') {
            steps {
                bat "dotnet restore ${workspace}\\OktaJenkinsCI.sln"
            }
        }
        
        stage('Clean') {
            steps {
                bat "msbuild.exe ${workspace}\\OktaJenkinsCI.sln" /nologo /nr:false /p:platform=\"x64\" /p:configuration=\"release\" /t:"clean"
            }
        }

        stage('Build') {
            steps {
                echo 'Building'
                bat 'dotnet publish --output bin/publish'
                bat 'bin\\publish\\OktaJenkinsCI.exe'
            }
        }
         stage('Test') {
            steps {
                echo 'Tesing'
            }
        }
         stage('Release') {
            steps {
                echo 'Release'
            }
        }
    }
}
