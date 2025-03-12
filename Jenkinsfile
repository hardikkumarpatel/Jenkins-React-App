pipeline {
    agent any
    stages {
         stage("Build") {
                steps {
                    sh "yarn"
                    sh "yarn run build"
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
