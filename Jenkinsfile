pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/kartik-2011/ScientificCalculator-DevOps.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t kaali2011/scientific-calculator .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push kaali2011/scientific-calculator'
            }
        }

        stage('Deploy with Ansible') {
            steps {
                sh 'ansible-playbook -i hosts deploy.yml'
            }
        }

    }
    post {
        failure {
            emailext (
                subject: "Build Failed: ${env.JOB_NAME}",
                body: "Something went wrong in build ${env.BUILD_NUMBER}",
                to: "your-email@gmail.com"
            )
        }
    }
}