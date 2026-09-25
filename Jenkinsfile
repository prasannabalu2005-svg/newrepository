pipeline {

parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['DEV', 'PROD'],
            description: 'Select deployment environment'
        )
    }
    
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Jenkins connected to GitHub!'
                    echo "Selected Environment: $
                    {params.ENVIRONMENT}"
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application...'
                sh 'node --check app.js'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t vehicle-spareparts:latest .'
            }
        }

        stage('Docker Hub Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        docker tag vehicle-spareparts:latest $DOCKER_USERNAME/vehicle-spareparts:latest
                        docker push $DOCKER_USERNAME/vehicle-spareparts:latest
                        docker logout
                    '''
                }
            }
        }

        stage('Success') {
            steps {
                echo 'Build, Test, Docker Build and Docker Hub Push successful!'
            }
        }
    }
}
//webhook test
