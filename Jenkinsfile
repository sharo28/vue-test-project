pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
                withCredentials([azureServicePrincipal('static-web-app')]) {
                    sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
                }
            }
        }
    }
}