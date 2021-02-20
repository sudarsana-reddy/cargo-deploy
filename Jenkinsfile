pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "System Maven"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', changelog: false, credentialsId: 'github_credentials', poll: false, url: 'https://github.com/sudarsana-reddy/cargo-deploy.git'

                // // Run Maven on a Unix agent.
                // sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                bat "mvn install"
                bat "mvn cargo:deploy"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    echo "successfully deployed"
                }
            }
        }
    }
}
