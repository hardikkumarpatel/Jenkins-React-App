pipeline {
    agent any
    tools {
      nodejs 'NodeJS'
    }
    environment {
        DEPLOY_DIR = "/root/var/www/html/jenkins-react-app"
        APP_NAME = "jenkins-react-app"
        PORT = "3005"
    }
    stages {
        stage("Build") {
            steps {
                echo "Building React App..."
                sh "npm install"
                sh "npm run build"
            }
        }
        
        stage("Deploy") {
            steps {
                echo "Deploying Build..."
                sh """
                    sudo mkdir -p ${DEPLOY_DIR}
                    sudo chown -R jenkins:jenkins ${DEPLOY_DIR}
                    sudo chmod -R 755 ${DEPLOY_DIR}
                    sudo cp -r ${WORKSPACE}/build/* ${DEPLOY_DIR}/
                """
            }
        }

        stage("Release") {
            steps {
                script {
                    echo "Managing PM2 Process..."
                    def pm2Check = sh(script: "sudo pm2 list | grep -w ${APP_NAME}", returnStatus: true)

                    if (pm2Check == 0) {
                        echo "PM2 process found. Restarting..."
                        sh "sudo pm2 restart ${APP_NAME}"
                    } else {
                        echo "No existing PM2 process found. Starting a new one..."
                        sh "sudo pm2 serve ${DEPLOY_DIR}/build ${PORT} --spa --name ${APP_NAME}"
                    }

                    sh "sudo pm2 save"
                    sh "sudo pm2 list"
                }
            }
        }
    }
}
