pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps{
                git url:"https://hardikkumarpatel@github.com/hardikkumarpatel/React-App-Demo.git",branch:"master"
            }
        }
         stage("Build") {
                steps {
                    sh "sudo yarn"
                    sh "sudo yarn run build"
                }
        }
        stage("Deploy") {
                steps {
                    sh "sudo rm -rf /root/var/www/html/jenkins-react-app"
                    sh "sudo cp -r ${WORKSPACE}/build/ /root/var/www/html/jenkins-react-app/"
                }
        }
    }
}
