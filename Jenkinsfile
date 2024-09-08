pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo "My client id is $AZURE_CLIENT_ID"
                echo "My tenant id is $AZURE_TENANT_ID"
                echo "My subscription id is $AZURE_SUBSCRIPTION_ID"
            }
        }
    }
}