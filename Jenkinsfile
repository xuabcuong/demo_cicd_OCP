pipeline {
    agent any

    environment {
        PROJECT = "demo"
        APP_NAME = "springboot-demo"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/xuabcuong/demo_cicd_OCP.git'
            }
        }

        stage('Build JAR') {
            steps {
                sh 'chmod +x gradlew'
                sh './gradlew clean build -x test'
            }
        }

        stage('Build Image on OpenShift') {
            steps {
                sh """
                oc project ${PROJECT}

                oc new-build --binary --name=${APP_NAME} \
                  --image-stream=java:17 \
                  --strategy=docker || true

                oc start-build ${A
