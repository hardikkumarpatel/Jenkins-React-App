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
                    sh "sudo pm2 list"
                    
                    def pm2Check = sh(script: "pm2 list | grep ${appName}", returnStatus: true)

                    if (pm2Check == 0) {
                        echo "PM2 process found. Restarting..."
                        sh "pm2 restart ${appName}"
                        sh "pm2 save"
                        sh "pm2 list"
                    } else {
                        echo "No existing PM2 process found. Starting a new one..."
                        sh "pm2 serve /var/www/html/jenkins-react-app/build 3005 --spa --name ${appName}"
                        sh "pm2 save"
                        sh "pm2 list"
                    }
                }
            }
        }
        
    }
}
