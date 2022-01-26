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
                bat 'dotnet build'
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
