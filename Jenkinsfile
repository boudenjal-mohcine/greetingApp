pipeline {
    agent any
    environment {
        REMOTE_PATH = ' /home/mohcineboudenjal'
        FILE_NAME = 'hello'
    }
    stages {
        stage('Static Analysis') {
            steps {
                echo 'Run the static analysis to the code'
            }
        }
        stage('Compile') {
            steps {
                echo 'Compile the source code'
            }
        }
        stage('Security Check') {
            steps {
                echo 'Run the security check against the application'
            }
        }
        stage('Run Unit Tests') {
            steps {
                echo 'Run unit tests from the source code'
            }
        }
        stage('Run Integration Tests') {
            steps {
                echo 'Run only crucial integration tests from the source code'
            }
        }
        stage('Publish Artifacts') {
            steps {
                script {
                    // Run commands on the production server
                    sh "ssh production-server \"touch ${REMOTE_PATH}/${FILE_NAME}\""
                }
            }
        }
    }
}
