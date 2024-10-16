pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout our repository
               git url: 'https://github.com/kevmach/Google-APIs-with-RestAssured.git'
 
            }
        }
        stage('Run Tests') {
            steps {
                // Run your API tests using Maven
                sh 'mvn clean test'
            }
        }
    }
    post {
        always {
            // Archive test reports and logs
            archiveArtifacts artifacts: '**/build/reports/**'
        }
        success {
            mail(
                to: 'degen_kev@proton.me', 
                subject: "Daily API Test Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Tests passed! Check details: ${env.BUILD_URL}"
            )
        }
        failure {
            mail(
                to: 'degen_kev@proton.me', 
                subject: "API Test Failure: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Tests failed. Check logs: ${env.BUILD_URL}"
            )
        }
    }
}
