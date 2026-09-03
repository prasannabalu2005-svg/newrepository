pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Jenkins connected to GitHub!'
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application...'
                sh 'node --check app.js'
            }
        }

        stage('Success') {
            steps {
                echo 'Build and Test successful!'
            }
        }
    }
}

