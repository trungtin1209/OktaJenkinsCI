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
/*        
        stage('Build') {
            steps {
                echo 'Building'
                bat 'dotnet publish --output bin/publish'
                bat 'bin\\publish\\OktaJenkinsCI.exe'
            }
        }
*/
        
        stage('Build') {
            steps {
                echo 'Building'
                bat 'dotnet build'
            }
        }
        
    stage('Running unit tests') {
        steps {
            bat "dotnet add ${workspace}\\OktaJenkinsCI.csproj package JUnitTestLogger --version 1.1.0"
            bat "dotnet test ${workspace}\\OktaJenkinsCI.csproj --logger \"junit;LogFilePath=\"${WORKSPACE}\"/TestResults/1.0.0.\"${env.BUILD_NUMBER}\"/results.xml\" --configuration release --collect \"Code coverage\""
            powershell '''
                $destinationFolder = \"$env:WORKSPACE/TestResults\"
                if (!(Test-Path -path $destinationFolder)) {New-Item $destinationFolder -Type Directory}
                $file = Get-ChildItem -Path \"$env:WORKSPACE/path-to-Unit-testing-project/name-of-unit-test-project/TestResults/*/*.coverage\"
                $file | Rename-Item -NewName testcoverage.coverage
                $renamedFile = Get-ChildItem -Path \"$env:WORKSPACE/path-to-Unit-testing-project/name-of-unit-test-project/TestResults/*/*.coverage\"
                Copy-Item $renamedFile -Destination $destinationFolder
            '''            
        }        
    }
        
         stage('Release') {
            steps {
                echo 'Release'
            }
        }
    }
}
