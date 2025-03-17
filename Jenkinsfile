pipeline {
    agent any
    tools {
      nodejs 'NodeJS'
    }
    stages {
         stage("Build") {
                steps {
                    echo "Building...."
                    sh "npm install"
                    sh "npm run build"
                }
        }
        stage("Deploy") {
                steps {
                    echo "Deployment...."
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
                    
                    def pm2Check = sh(script: "sudo pm2 list | grep ${appName}", returnStatus: true)

                    if (pm2Check == 0) {
                        echo "PM2 process found. Restarting..."
                        sh "sudo pm2 restart ${appName}"
                        sh "sudo pm2 list"
                    } else {
                        echo "No existing PM2 process found. Starting a new one..."
                        sh "sudo pm2 serve /var/www/html/jenkins-react-app/build 3005 --spa --name ${appName}"
                        sh "sudo pm2 save"
                        sh "sudo pm2 list"
                    }
                }
            }
        }
        
    }
}
