pipeline {
    agent any

    tools {
        maven 'maven-01'   // 👈 your Maven name
        jdk 'JDK'          // keep your configured JDK name
    }

    environment {
        GITHUB_CREDENTIALS = credentials('github-creds')
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/shanifm2002/demo-jenk.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deploy to GitHub Packages') {
            steps {
                sh """
                mvn deploy \
                -Dusername=$GITHUB_CREDENTIALS_USR \
                -Dpassword=$GITHUB_CREDENTIALS_PSW
                """
            }
        }
    }

    post {
        success {
            echo 'Build & Deployment Successful!'
        }
        failure {
            echo 'Build Failed!'
        }
    }
}
