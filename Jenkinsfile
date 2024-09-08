pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                withCredentials([azureServicePrincipal('static-web-app')]) {
                    sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID --allow-no-subscriptions'
                    sh 'az account set --subscription $AZURE_SUBSCRIPTION_ID'
                }
                sh 'npm install -D @azure/static-web-apps-cli'
                sh 'npx swa init --yes'
                sh 'npx swa build'
                sh 'npx swa login --resource-group test-statc-web-apps --app-name vue-test'
                sh 'swa deploy ./dist --env production --deployment-token 2cf1a9fafee37b6b95972ab45bd36bb601ea3ea8a358c1a9524078dc78ce0c355-4f431a87-e2f2-4c6c-a047-c5ac431238e0000292686'
            }
        }
    }
}