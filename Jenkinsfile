pipeline {
    agent any
    
    stages {
        stage('Setup Environment') {
            steps {
                script {
                    sh '''
                      docker-compose up -d 
                      PowerShell Start-Sleep -s 30
                      start java "-Dspring.datasource.url=jdbc:mysql://localhost:3306/app" -jar artifacts/aqa-shop.jar
                      PowerShell Start-Sleep -s 60
                      
                    '''
                }
            }
        }

        stage('Build and Test') {
            steps {
                script {
                    sh './gradlew "-Ddb.url=jdbc:mysql://localhost:3306/app" test --info -Dselenide.headless=true'
                }
            }
        }
    }
}
