pipeline {
    agent any
    environment {
        JENKINS_SSH_KEY = '/var/lib/jenkins/.ssh/id_rsa'
        REMOTE_USER = 'mohcineboudenjal'
        REMOTE_HOST = 'production-server'
        REMOTE_PATH = '/home/mohcineboudenjal/smartassurance/smart-assurance-test'
        JAR_NAME = 'greeting'  // Replace with your actual jar name
    }

    stages {
        stage('Test Connect SSH') {
            steps {
                script {
                    // Connect to the production server using SSH
                    sh """
                        ssh -i ${JENKINS_SSH_KEY} -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_HOST} '
                            mkdir -p ${REMOTE_PATH}/${JAR_NAME} &&
                            echo \"FROM openjdk:17-alpine\" > ${REMOTE_PATH}/${JAR_NAME}/Dockerfile &&
                            echo \"ARG JAR_FILE=target/${JAR_NAME}-0.0.1-SNAPSHOT.jar\" >> ${REMOTE_PATH}/${JAR_NAME}/Dockerfile &&
                            echo \"WORKDIR /opt/app\" >> ${REMOTE_PATH}/${JAR_NAME}/Dockerfile &&
                            echo \"COPY ${JAR_NAME} app.jar\" >> ${REMOTE_PATH}/${JAR_NAME}/Dockerfile &&
                            echo 'ENTRYPOINT ["java","-jar","app.jar"]' >> ${REMOTE_PATH}/${JAR_NAME}/Dockerfile
                        '
                    """
                }
            }
        }

        stage('Build and Copy JAR') {
            steps {
                script {
                    // Build the app locally
                    sh "mvn clean install"

                    // Copy the JAR to the remote path
                    sh "scp -i ${JENKINS_SSH_KEY} -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/java_project/target/${JAR_NAME}-0.0.1-SNAPSHOT.jar ${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_PATH}/${JAR_NAME}"
                }
            }
        }

        stage('reload docker') {
    steps {
        script {
            sh 'docker rm $(docker ps -a -q)'
            sh '''
                cd ${REMOTE_PATH} &&
                docker run --rm -v /var/run/docker.sock:/var/run/docker.sock -v "$PWD:$PWD" -w="$PWD" docker/compose:1.25.5 up
            '''
        }
    }

    }
}
