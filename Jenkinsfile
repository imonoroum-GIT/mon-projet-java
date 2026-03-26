pipeline {
    agent { label 'master' }
    
    tools {
        maven 'M3'
    }

    environment {
        IMG='mon-projet-java:${env.BUILD_ID}'
        CT_NAME='mon-projet-java-container"
    }

    stages {
        stage('Compilation') {
            steps {
                sh 'mvn clean package'
            }
        }

        Stage('Build docker image'){
            steps {
                sh 'docker build -t ${IMG} .'
            }
        }

        Stage ('deploiement'){
            steps {
                sh 'docker stop ${CT_NAME} ||true'
                sh 'docker rm ${CT_NAME} || true'
                sh 'docker run -d --name ${CT_NAME} ${IMG}'
            }
        }
    }

Post {
    success {
        echo "ca fonctionne"
        sh 'docker ps | grep ${CT_NAME}'
    }
}
}
