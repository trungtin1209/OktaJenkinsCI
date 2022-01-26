pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Build') {
            steps {
                echo 'Building'
                bat 'dotnet publish --output bin/publish'
                bat 'cd bin'
                bat 'cd publish'
                bat 'OktaJenkinsCI.exe'
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
