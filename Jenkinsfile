pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/zdmooc/devfile-sample-python-basic.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Commands to build your application, for example:
                    sh 'oc start-build python-app --from-dir=. --follow -n test'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Commands to deploy your application, for example:
                    sh 'oc rollout latest dc/python-app -n test'
                }
            }
        }
    }
}
