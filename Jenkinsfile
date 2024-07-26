pipeline {
    agent any

    environment {
        registry = "image-registry.openshift-image-registry.svc:5000"
        project = "test"
        app = "python-app"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/votre-repo/python-app.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    def buildConfig = openshift.selector("bc", "${app}")
                    buildConfig.startBuild("--from-dir=.", "--follow").logs("-f")
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def dc = openshift.selector("dc", "${app}")
                    dc.rollout().latest()
                    dc.rollout().status()
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Ajoutez ici vos tests spécifiques
                    echo 'Tests are running...'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
