pipeline {
    agent any
    tools {
      nodejs 'NodeJS'
    }
    stages {
         stage("Build") {
                steps {
                    sh "npm install"
                    sh "npm run build"
                }
        }
        stage("Deploy") {
                steps {
                    sh "mkdir -p /var/www/html/jenkins-react-app"
                    sh "chown -R jenkins:jenkins /var/www/html/jenkins-react-app"
                    sh "chmod -R 755 /var/www/html/jenkins-react-app"
                    sh "cp -r ${WORKSPACE}/build/ /var/www/html/jenkins-react-app/"
                }
        }
        stage("Release") {
            steps {
                script {
                    def appName = "jenkins-react-app"
                    def pm2Check = sh(script: "pm2 list | grep ${appName}", returnStatus: true)

                    if (pm2Check == 0) {
                        echo "PM2 process found. Restarting..."
                        sh "pm2 restart ${appName}"
                    } else {
                        echo "No existing PM2 process found. Starting a new one..."
                        sh "/root/.nvm/versions/node/v20.18.2/bin/pm2 serve /var/www/html/jenkins-react-app/ 3005 --span --name ${appName}"
                    }
                }
            }
        }
    }
}
