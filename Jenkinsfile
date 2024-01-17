pipeline {
    agent any
    environment {
        REMOTE_PATH = '/home/mohcineboudenjal'
        FILE_NAME = 'helloo'
        JENKINS_SSH_KEY = '/var/lib/jenkins/.ssh/id_rsa'  // Adjust the path accordingly
    }
    stages {
        stage('Test Connect SSH') {
            steps {
                script {
                    // Run commands on the production server
                    sh "ssh -i ${JENKINS_SSH_KEY} -o StrictHostKeyChecking=no mohcineboudenjal@production-server touch ${REMOTE_PATH}/${FILE_NAME}"
                }
            }
        }
    }
}
