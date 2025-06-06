pipeline {
    agent any

    stages {
        stage('Run Postman Collection') {
            steps {
                // Change into the folder where your collection + environment files live
                dir('C:\\Users\\nagar\\.jenkins\\Postman_APItest') {
                    // Have Newman export as “gitapireport.html”
                    bat '''
                        newman run SwaggerAPI.postman_collection.json ^
                            -e QAEnvironmentS.postman_environment.json ^
                            -r html ^
                            --reporter-html-export gitapireport.html ^
                            || exit 0
                    '''.stripIndent()

                    // Copy the generated gitapireport.html into the Jenkins workspace
                    bat 'copy /Y gitapireport.html "%WORKSPACE%\\gitapireport.html"'
                }
            }
        }

        stage('Archive Report') {
            steps {
                // Archive the copied gitapireport.html from the workspace
                archiveArtifacts artifacts: 'gitapireport.html', fingerprint: true
            }
        }
    }
}