pipeline {
    agent any

    environment {
        // Define reusable environment variables
        BUILD_DIR = 'target'
        ARTIFACT = 'myapp.jar'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                // Checkout from Git (customize your repo URL)
                git branch: 'main', url: 'https://github.com/your-org/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                // Use Maven to build (example)
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }
        }

        stage('Code Quality Check') {
            steps {
                echo 'Running static code analysis...'
                // Example: SonarQube or custom scripts
                // sh 'mvn sonar:sonar'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application...'
                // Optional if already packaged during build
                sh 'mvn package'
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Archiving the built artifact...'
                archiveArtifacts artifacts: "${BUILD_DIR}/${ARTIFACT}", fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying
