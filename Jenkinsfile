pipeline {
    agent any

    environment {
        APP_NAME = 'myapp'
        BUILD_DIR = 'build'
        DEPLOY_USER = 'ubuntu'
        DEPLOY_HOST = 'your.server.ip'
        DEPLOY_PATH = '/var/www/myapp'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh '''
                    echo "[INFO] Creating build directory..."
                    mkdir -p ${BUILD_DIR}
                    echo "Sample app file" > ${BUILD_DIR}/${APP_NAME}.txt
                    echo "[INFO] Build completed: ${BUILD_DIR}/${APP_NAME}.txt"
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh '''
                    echo "[TEST] Starting mock test..."
                    sleep 1
                    if [ -f ${BUILD_DIR}/${APP_NAME}.txt ]; then
                        echo "[TEST] File exists: PASS"
                    else
                        echo "[TEST] File missing: FAIL"
                        exit 1
                    fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh '''
                    echo "[DEPLOY] Packaging artifact..."
                    tar -czf ${APP_NAME}.tar.gz ${BUILD_DIR}

                    echo "[DEPLOY] Copying to server..."
                    scp -i ~/.ssh/your-ec2-key.pem ${APP_NAME}.tar.gz ${DEPLOY_USER}@${DEPLOY_HOST}:${DEPLOY_PATH}/

                    echo "[DEPLOY] Extracting on remote..."
                    ssh -i ~/.ssh/your-ec2-key.pem ${DEPLOY_USER}@${DEPLOY_HOST} "
                        mkdir -p ${DEPLOY_PATH}/release &&
                        tar -xzf ${DEPLOY_PATH}/${APP_NAME}.tar.gz -C ${DEPLOY_PATH}/release
                    "

                    echo "[DEPLOY] Done."
                '''
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
