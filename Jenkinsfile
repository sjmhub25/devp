pipeline {
    agent any

    environment {
        IMAGE = "sowjanya2510/devp:v1"
        CREDS = "dockerhub-creds"
        GIT_REPO = "https://github.com/sjmhub25/devp.git"
        GIT_BRANCH = "main" // Ensure this matches your GitHub branch
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: "${GIT_BRANCH}", url: "${GIT_REPO}"
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
                withCredentials([usernamePassword(
                    credentialsId: CREDS,
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
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
