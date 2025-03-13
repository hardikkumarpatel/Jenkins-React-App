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
                    sh "rm -rf /root/var/www/html/jenkins-react-app"
                    sh "cp -r ${WORKSPACE}/build/ /root/var/www/html/jenkins-react-app/"
                }
        }
    }
}
