pipeline {
    agent any
    
    stages {
        stage('Setup Environment') {
            steps {
                script {
                        - docker-compose up -d
                        - sleep 30
                        - java -Dspring.datasource.url=jdbc:mysql://localhost:3306/app -jar artifacts/aqa-shop.jar &
                        - sleep 60   
                }
            }
        }

        stage('Build and Test') {
            steps {
                script {
                    - ./gradlew "-Ddb.url=jdbc:mysql://localhost:3306/app" test --info -Dselenide.headless=true'
                }
            }
        }
    }
}
