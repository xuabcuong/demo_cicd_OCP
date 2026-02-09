pipeline {
    agent any

    environment {
        PROJECT = "demo"
        APP_NAME = "springboot-demo"
        REGISTRY = "image-registry.openshift-image-registry.svc:5000"
        IMAGE = "${REGISTRY}/${PROJECT}/${APP_NAME}:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/xuabcuong/demo_cicd_OCP.git'
            }
        }

         stage('Build JAR') {
                    steps {
                        sh 'chmod +x gradlew'
                        sh './gradlew clean build -x test'
                    }
                }

        stage('Build & Push Image') {
            steps {
                sh """
                oc project ${PROJECT}
                docker build -t ${IMAGE} .
                docker push ${IMAGE}
                """
            }
        }

        stage('Deploy') {
            steps {
                sh """
                oc apply -f k8s/deployment.yaml
                oc apply -f k8s/service.yaml
                """
            }
        }
    }
}
