pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh "docker build -t elnabawy/my-web-app:test-${env.BUILD_ID} ."
                withCredentials([usernamePassword(credentialsId: 'docker-cre', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "docker login -u $USERNAME -p $PASSWORD"
                }
                sh "docker push elnabawy/my-web-app:test-${env.BUILD_ID}"
            }
        }
        stage('deploy') {
            steps {
                sh "docker stop web_app"
                sh "docker rm web_app"
                sh "docker run -itd -p 8085:80 --name web_app elnabawy/my-web-app:test-${env.BUILD_ID}"
            }
        }
    }
}
