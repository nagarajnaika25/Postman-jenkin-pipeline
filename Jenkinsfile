pipeline {
    agent any

    stages {
        stage('Run Postman Collection') {
            steps {
                bat '''
                    newman run SwaggerAPI.postman_collection.json ^
                        -e QAEnvironmentS.postman_environment.json ^
                        -r html ^
                        --reporter-html-export gitapireport.html
                '''
            }
        }

        stage('Archive Report') {
            steps {
                archiveArtifacts artifacts: 'gitapireport.html', fingerprint: true
            }
        }
    }
}
