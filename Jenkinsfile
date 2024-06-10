pipeline {
    agent any
    tools {
        jdk  'default'
        maven 'default'
    }

    parameters {
            string(name: 'BRANCH', defaultValue: 'main', description: 'parameterized file',
            defaultValue: 'marshmellow')
        }

        environment {
            BUILD_NUMBER = "${env.BUILD_NUMBER}"
        }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/RajeshPeddada/jenkins-training'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build') {
            steps {
                    echo 'Building ${env.BUILD_NUMBER}...'
                sh 'mvn clean package'
            }
        }

        stage('Archive'){
            steps{
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }

    }

    post {
        success {
            echo 'Build was successful'
        }

        failure {
            echo 'Build failed'
        }
    }


}