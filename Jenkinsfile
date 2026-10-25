pipeline {
    agent any

    options {
        skipStagesAfterUnstable()
    }

    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout Source Code') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-hw7-ssh',
                    url: 'git@github.com:s3bas9221/jenkins-springboot-hw7.git'
            }
        }

        stage('Test') {
            steps {
                sh 'git --version'
                sh 'mvn --version'
                sh 'mvn clean test'
            }
        }

        stage('Build and Package') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar',
                                 fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }

        success {
            echo 'Build successful!'
        }

        failure {
            echo 'Build failed!'
        }
    }
}