pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/saikrishnagorijavolu/Sai.git'
            }
        }
        
        stage('Build and Test') {
            steps {
                // Add your build and test commands here
                // For example:
                // sh 'npm install'
                // sh 'npm test'
            }
        }
        
        stage('Deploy to Test Environment') {
            environment {
                AZURE_CREDENTIALS = credentials('SAI')
                AZURE_RESOURCE_GROUP = 'sampleweb42_group'
                AZURE_APP_SERVICE_NAME = 'sampleweb42'
            }
            
            steps {
                script {
                    azureLoginServicePrincipal()
                    azureWebAppPublish appName: AZURE_APP_SERVICE_NAME, resourceGroup: AZURE_RESOURCE_GROUP, filePath: 'path-to-artifact'
                }
            }
        }
        
        stage('Deploy to Stage Environment') {
            environment {
                 AZURE_CREDENTIALS = credentials('SAI')
                AZURE_RESOURCE_GROUP = 'sampleweb42_group'
                AZURE_APP_SERVICE_NAME = 'sampleweb42'
            }
            
            steps {
                script {
                    azureLoginServicePrincipal()
                    azureWebAppPublish appName: AZURE_APP_SERVICE_NAME, resourceGroup: AZURE_RESOURCE_GROUP, filePath: 'path-to-artifact'
                }
            }
        }
        
        stage('Deploy to Prod Environment') {
            environment {
                 AZURE_CREDENTIALS = credentials('SAI')
                AZURE_RESOURCE_GROUP = 'sampleweb42_group'
                AZURE_APP_SERVICE_NAME = 'sampleweb42'
            }
            
            steps {
                script {
                    azureLoginServicePrincipal()
                    azureWebAppPublish appName: AZURE_APP_SERVICE_NAME, resourceGroup: AZURE_RESOURCE_GROUP, filePath: 'path-to-artifact'
                }
            }
        }
    }
    
    post {
        always {
            azureLogout()
        }
    }
}

def azureLoginServicePrincipal() {
    withCredentials([azureServicePrincipal(credentialsId: 'SAI', displayName: 'sampleweb42_group')]) {
        sh 'az login --service-principal -u 3dab05d1-c927-412c-a512-5085ae2b727e -p f830e9a3-51cc-45f0-9e02-77db9a1a04e1 --tenant db41ed96-0ae4-49e3-be3b-74fe16e973cd'
    }
}

def azureLogout() {
    sh 'az logout'
}
