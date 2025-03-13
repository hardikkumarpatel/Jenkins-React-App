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
                    sh "mkdir -p /root/var/www/html/jenkins-react-app"
                    sh "chown -R jenkins:jenkins /root/var/www/html/jenkins-react-app"
                    sh "chmod -R 755 /root/var/www/html/jenkins-react-app"
                    sh "cp -r ${WORKSPACE}/build/ /root/var/www/html/jenkins-react-app/"
                }
        }
    }
}
