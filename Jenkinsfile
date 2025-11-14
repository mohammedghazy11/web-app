pipeline {
    agent { label 'slave' }

    stages {
        stage('Build') {
            steps {
                sh "docker build -t elnabawy/web-app:1.1.${env.BUILD_ID} ."
                withCredentials([usernamePassword(credentialsId: 'docker-cred', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "docker login -u $USERNAME -p $PASSWORD"
                    sh "docker push elnabawy/web-app:1.1.${env.BUILD_ID}"
                }
            }
        }
        stage('deploy') {
            steps {
                sh "docker run -itd -p 8085:80 elnabawy/web-app:1.1.${env.BUILD_ID}"
            }
        }
    }
}
