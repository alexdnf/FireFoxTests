pipeline {
    agent any

    stages {
        stage('Start Containers') {
            steps {
                bat 'docker-compose up -d'
                bat 'Start-Sleep -Seconds 30'
            }
        }

        stage('Run Application') {
            steps {
                bat 'start java -Dspring.datasource.url=jdbc:mysql://localhost:3306/app -jar artifacts/aqa-shop.jar'
                bat 'Start-Sleep -Seconds 60'
            }
        }

        stage('Run Tests') {
            steps {
                bat './gradlew "-Ddb.url=jdbc:mysql://localhost:3306/app" test --info -Dselenide.headless=true'
            }
        }
    }
}
