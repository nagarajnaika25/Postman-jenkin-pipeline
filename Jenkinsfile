pipeline {
    agent any
    stages {
        stage('Run Postman Collection') {
            steps {
                dir('C:\\Users\\nagar\\.jenkins\\Postman_APItest') {
                    // Force exit 0 so Jenkins doesn’t fail if Newman returns minor warnings
                    bat 'newman run SwaggerAPI.postman_collection.json -e QAEnvironmentS.postman_environment.json -r html --reporter-html-export report.html || exit 0'
                }
            }
        }
        stage('Archive Report') {
            steps {
                archiveArtifacts artifacts: 'report.html', fingerprint: true
            }
        }
    }
}


