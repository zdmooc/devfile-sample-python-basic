pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/zdmooc/devfile-sample-python-basic.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Commande pour lancer la build de votre application
                    sh 'oc start-build python-app --from-dir=. --follow -n test'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Commande pour déployer votre application
                    sh 'oc rollout latest dc/python-app -n test'
                }
            }
        }
    }
}
