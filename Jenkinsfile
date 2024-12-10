pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker-compose up -d'
                sleep(time: 30, unit: 'SECONDS')
                sh 'java -Dspring.datasource.url=jdbc:mysql://localhost:3306/app -jar artifacts/aqa-shop.jar &'
                sleep(time: 60, unit: 'SECONDS')
                sh './gradlew -Ddb.url=jdbc:mysql://localhost:3306/app test --info -Dselenide.headless=true'
            }
        }
    }
}
