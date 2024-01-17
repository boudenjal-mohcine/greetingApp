pipeline {
    agent any
    environment {
        REMOTE_PATH = '/home/mohcineboudenjal'
        FILE_NAME = 'helloo'
    }
    stages {
        stage('Static Analysis') {
            steps {
                echo 'Run the static analysis on the code'
                // Add commands for static analysis here
            }
        }
        stage('Compile') {
            steps {
                echo 'Compile the source code'
                // Add commands for compilation here
            }
        }
        stage('Security Check') {
            steps {
                echo 'Run the security check against the application'
                // Add commands for security check here
            }
        }
        stage('Run Unit Tests') {
            steps {
                echo 'Run unit tests from the source code'
                // Add commands for running unit tests here
            }
        }
        stage('Run Integration Tests') {
            steps {
                echo 'Run only crucial integration tests from the source code'
                // Add commands for running integration tests here
            }
        }
        stage('Test Connect SSH') {
            steps {
                echo 'Testing SSH connection and touching file on the production server'
                script {
                    // Run commands on the production server
                    
                 sh "ssh -o StrictHostKeyChecking=no production-server touch ${REMOTE_PATH}/${FILE_NAME}"

                }
            }
        }
    }
}
