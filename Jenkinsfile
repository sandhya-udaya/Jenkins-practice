pipeline{
    agent any

    parameters{
        string{
            name:'APP_PORT',
            defaultValue:'3000',
            description:'Server Port'
        }
    }

    environment{
        IMAGE_NAME='jenkins-demo-app'
    }

    stages{
        stage('Checkout'){
            steps{
                echo 'Checking out Source Code From Git Repo'
                Checkout scm
            }
        }
        stage('Dependencies'){
            steps{
                bat 'npm insall'
            }
        }
        stage('Test App'){
            steps{
                bat 'npm test'
            }
        }
        stage('Build'){
            steps{
                bat 'docker build -t %IMAGE_NAME%:%BUILD_NUMBER% .'
            }
        }
        stage('Run Container'){
            steps{
                bat '''
                docker run -d --name node-app-%BUILD_NUMBER% -p %APP_PORT%:3000 %IMAGE-NAME%:%BUILD_NUMBER%'
                '''

            }

        }
        stage('verify'){
            steps{
                bat '''
                echo APP Deployed Successfully
                echo Open http://localhost:%APP_PORT%
                docker ps
                '''
            }
        }
    }
}