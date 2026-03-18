pipeline {
    agent {
        docker {
            image 'docker:20.10.16'
            args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
        IMAGE = "sowjanya2510/devp:v1"
        CREDS = "dockerhub-creds"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sjmhub25/devp.git'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t devp .'
            }
        }
        stage('Tag') {
            steps {
                sh 'docker tag devp sowjanya2510/devp:v1'
            }
        }
        stage('Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: CREDS, usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }
        stage('Push') {
            steps {
                sh 'docker push sowjanya2510/devp:v1'
            }
        }
    }
}
