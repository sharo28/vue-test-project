pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                withCredentials([azureServicePrincipal('static-web-app')]) {
                    sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID --allow-no-subscriptions'
                }
                sh 'npm install -D @azure/static-web-apps-cli'
                sh 'npx swa init --yes'
                sh 'npx swa build'
                sh 'npx swa login --resource-group test-statc-web-apps --app-name vue-test'
                sh 'npx swa deploy --env production'
            }
        }
    }
}