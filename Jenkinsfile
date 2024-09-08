pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                withCredentials([azureServicePrincipal('static-web-app')]) {
                    sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID --allow-no-subscriptions'
                }
                echo '1'
                sh 'npx swa init --yes'
                echo '2'
                sh 'npx swa build'
                echo '3'
                sh 'npx swa login --resource-group test-statc-web-apps --app-name vue-test'
                echo '4'
            }
        }
    }
}