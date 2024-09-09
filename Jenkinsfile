pipeline {
    agent any
    options {
        timeout(time: 1, unit: 'HOURS') 
    }
    stages {
        stage('staging') {
            steps {
                withCredentials([azureServicePrincipal('static-web-app')]) {
                    sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID --allow-no-subscriptions'
                    sh 'az account set --subscription $AZURE_SUBSCRIPTION_ID'
                }
                sh 'npm install -D @azure/static-web-apps-cli'
                sh 'npx swa init --yes'
                sh 'npx swa build'
                sh 'npx swa login --resource-group test-statc-web-apps --app-name vue-test'
                sh 'env DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=1 npx swa deploy --no-use-keychain --verbose=silly --env staging --deployment-token 9d427fcac1d4fd84930536fc7cb44b9da6061f20a394f68162554852e9a629545-c960fb77-894a-4909-b178-10073973e691000292686'
                sh 'az logout'
            }
        }
        stage('release') {
            steps {
                withCredentials([azureServicePrincipal('static-web-app')]) {
                    sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID --allow-no-subscriptions'
                    sh 'az account set --subscription $AZURE_SUBSCRIPTION_ID'
                }
                sh 'npm install -D @azure/static-web-apps-cli'
                sh 'npx swa init --yes'
                sh 'npx swa build'
                sh 'npx swa login --resource-group test-statc-web-apps --app-name vue-test'
                sh 'env DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=1 npx swa deploy --no-use-keychain --verbose=silly --env production --deployment-token 9d427fcac1d4fd84930536fc7cb44b9da6061f20a394f68162554852e9a629545-c960fb77-894a-4909-b178-10073973e691000292686'
                sh 'az logout'
            }
        }
    }
}