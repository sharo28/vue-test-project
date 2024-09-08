pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                withCredentials([azureServicePrincipal('static-web-app')]) {
                    sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID --subscription $AZURE_SUBSCRIPTION_ID'
                }
            }
        }
    }
}