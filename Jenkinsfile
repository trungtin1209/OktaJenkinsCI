pipeline {
    agent 
    {
        docker{
            image 'mcr.microsoft.com/windows/server:ltsc2022'
        }
    }

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
        
//#        stage('Clean') {
//#            steps {
//#                bat "msbuild ${workspace}\\OktaJenkinsCI.sln /nologo /nr:false /p:platform=\"x64\" /p:configuration=\"release\" /t:clean"
//#            }
//#        }
   
/* 
        stage('Increase version') {
                steps {
                echo "${env.BUILD_NUMBER}"
                powershell '''
                    $xmlFileName = "Package.appxmanifest"     
                    [xml]$xmlDoc = Get-Content $xmlFileName
                    $version = $xmlDoc.Package.Identity.Version
                    $trimmedVersion = $version -replace '.[0-9]+$', '.'
                    $xmlDoc.Package.Identity.Version = $trimmedVersion + ${env:BUILD_NUMBER}
                    echo 'New version:' $xmlDoc.Package.Identity.Version
                    $xmlDoc.Save($xmlFileName)
                    '''
            }
        }
*/
   
        stage('Build') {
            steps {
                echo 'Building'
                bat 'dotnet publish --output bin/publish'
                bat 'bin\\publish\\OktaJenkinsCI.exe'
            }
        }
 
        
         stage('Release') {
            steps {
                echo 'Release'
            }
        }
    }
}
