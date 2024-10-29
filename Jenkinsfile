pipeline {
    agent any
    environment {
        GITHUB_CREDENTIALS = credentials('GitHub') // GitHub credentials ID in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sharu1301/Gitlab-CI-Jenkins-Migration.git', credentialsId: "${GITHUB_CREDENTIALS}"
            }
        }
        stage('Build') {
            steps {
                script {
                    sh './gradlew clean build'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh './gradlew test'
                }
            }
        }
        stage('Package') {
            steps {
                script {
                    sh './gradlew assemble'
                }
            }
        }
        stage('Store Artifact') {
            steps {
                archiveArtifacts artifacts: '**/build/libs/*.jar', allowEmptyArchive: false
            }
        }
    }
    post {
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
