pipeline {

    agent none

    stages {

        stage('Checkout') {
            agent any
            steps {
                git(
                    url: 'https://github.com/DineshReddy6303/java-maven-project.git',
                    branch: 'main',
                    credentialsId: 'github-credentials'
                )
            }
        }

        stage('Build') {
            agent {
                docker {
                    image 'maven:3.8.8-eclipse-temurin-17'
                    args '--entrypoint=""'
                }
            }
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'maven:3.8.8-eclipse-temurin-17'
                    args '--entrypoint=""'
                }
            }
            steps {
                sh 'mvn test'
            }
        }

        stage('Docker Build') {
            agent any
            steps {
                sh '''
                    docker build -t java-maven-app:${BUILD_NUMBER} .
                '''
            }
        }

        stage('Run Docker Container') {
            agent any
            steps {
                sh '''
                    docker run --rm java-maven-app:${BUILD_NUMBER}
                '''
            }
        }
    }
}
