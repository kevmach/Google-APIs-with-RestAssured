pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout our repository
                https://github.com/kevmach/Google-APIs-with-RestAssured.git, branch: 'master'
            }
        }
        stage('Run Tests') {
    steps {
        // Run your API tests using Maven
        sh 'mvn clean test'
    }
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
                to: 'kelvinmachinda6@gmail.com',
                subject: "Daily API Test Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Tests passed! Check details: ${env.BUILD_URL}"
            )
        }
        failure {
            mail(
                to: 'kelvinmachinda6@gmail.com',
                subject: "API Test Failure: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Tests failed. Check logs: ${env.BUILD_URL}"
            )
        }
    }
}
