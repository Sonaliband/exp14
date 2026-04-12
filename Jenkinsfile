pipeline {
    agent any

    triggers {
        pollSCM('* * * * *') // Poll the SCM every 5 minutes
    }

    environment {
        IMAGE_NAME = "devops-app" 
        CONTAINER_NAME = "devops-container"
        APP_PORT = "5000" // Define any environment variables here
    }
       

    stages {
        stage('Build Docker Image') {
            steps {
                bat "docker build --no-cache -t %IMAGE_NAME% ."
                // Add build steps here
            }
        }
        stage('Stop Existing Containers') {
            steps {
                bat '''
                for /f "tokens=*" %%i in ('docker ps -q') do docker stop %%i
                for /f "tokens=*" %%i in ('docker ps -aq') do docker rm %%i
                '''
                // Add test steps here
            }
        }
        stage('Run New Container') {
            steps {
                bat "docker run -d --name %CONTAINER_NAME% -p %APP_PORT%:%APP_PORT% %IMAGE_NAME%"
                // Add deploy steps here
            }
        }
    }
}