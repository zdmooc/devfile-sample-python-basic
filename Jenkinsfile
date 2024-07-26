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
                    // Construire l'image Docker et l'envoyer à l'image stream OpenShift
                    sh 'oc start-build python-app --from-dir=. --follow -n test'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Appliquer le fichier de déploiement
                    sh 'oc apply -f deploy.yaml -n test'
                    // Redémarrer le déploiement pour appliquer les nouveaux changements
                    sh 'oc rollout restart deployment/my-python -n test'
                }
            }
        }
    }
}
