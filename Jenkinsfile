pipeline {
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: gradle
    image: registry.redhat.io/ubi8/openjdk-17
    command:
    - cat
    tty: true
"""
    }
  }

  stages {
    stage('Build') {
      steps {
        container('gradle') {
          sh 'java -version'
          sh 'chmod +x gradlew'
          sh './gradlew clean build -x test'
        }
      }
    }
  }
}
