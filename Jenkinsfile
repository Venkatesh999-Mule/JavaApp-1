pipeline {
    agent any

    stages {

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t hello-devops .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker stop hello-devops || true'
                sh 'docker rm hello-devops || true'
                sh 'docker run -d -p 8080:8080 --name hello-devops hello-devops'
            }
        }

    }

    post {
        success { echo 'App is running! Visit http://$(curl ifconfig.me):8080' }
        failure { echo 'Something went wrong. Check logs above.' }
    }
}