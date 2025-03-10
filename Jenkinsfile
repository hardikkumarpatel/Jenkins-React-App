pipeline {
    agent any
    stages {
        stage('Checkout Latest Code') {
            steps {
                dir('/root/var/www/html/React-App-Demo') {
                    sh 'git checkout master' // Ensure we are on master branch
                    sh 'git pull origin master' // Pull latest code from remote
                }
            }
        }
        stage('Clean Previous Build') {
            steps {
                dir('/root/var/www/html/React-App-Demo') {
                    sh 'rm -rf build' // Remove old build directory
                }
            }
        }
        stage('Install Dependencies & Build') {
            steps {
                dir('/root/var/www/html/React-App-Demo') {
                    sh 'yarn'  // Install dependencies
                    sh 'yarn run build' // Build the project
                }
            }
        }
        // stage('Deploy') {
        // }
    }
}
