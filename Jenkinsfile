pipeline {
    agent any // Specifies where the pipeline will run. 'any' means on any available agent.

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Add your build commands here, e.g.,
                // sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add your test commands here, e.g.,
                // sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Add your deployment commands here, e.g.,
                // sh 'scp target/myapp.jar user@server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed, please check logs.'
        }
    }
}
