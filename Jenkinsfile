pipeline {
    agent any
    stages {
        stage('Checkout Latest Code') {
            steps {
                script { echo "Inside the checkout stage..." }
                dir('/root/var/www/html/React-App-Demo') {
                    sh 'git checkout master' // Ensure we are on master branch
                    sh 'git pull origin master' // Pull latest code from remote
                }
            }
        }
        stage('Clean Previous Build') {
            script { echo "Inside the clean build stage..." }
            steps {
                dir('/root/var/www/html/React-App-Demo') {
                    sh 'rm -rf build' // Remove old build directory
                }
            }
        }
        stage('Install Dependencies & Build') {
            script { echo "Inside the build installation stage..." }
            steps {
                dir('/root/var/www/html/React-App-Demo') {
                    sh 'yarn'  // Install dependencies
                    sh 'yarn run build' // Build the project
                }
            }
        }
        stage('Deploy') {
            script { echo "Inside the deployment stage..." }
        }
    }
}
