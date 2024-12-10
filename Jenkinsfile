pipeline {
    agent any

    stages {
        stage('Start Containers') {
            steps {
                bat 'docker-compose up -d'
                bat 'timeout /T 30'
            }
        }

        stage('Run Application') {
            steps {
                bat 'start java -Dspring.datasource.url=jdbc:mysql://localhost:3306/app -jar artifacts/aqa-shop.jar'
                bat 'timeout /T 60'
            }
        }

        stage('Run Tests') {
            steps {
                bat './gradlew "-Ddb.url=jdbc:mysql://localhost:3306/app" test --info -Dselenide.headless=true'
            }
        }
    }
}
