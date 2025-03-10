pipeline {
    agent any
    stages {
        stage('Checkout Latest Code') {
            steps {
                dir('/var/www/html/Admin-Dashboard') {
                    sh 'git checkout master' // Ensure we are on master branch
                    sh 'git pull origin master' // Pull latest code from remote
                }
            }
        }
        stage('Clean Previous Build') {
            steps {
                dir('/var/www/html/Admin-Dashboard') {
                    sh 'rm -rf build' // Remove old build directory
                }
            }
        }
        stage('Install Dependencies & Build') {
            steps {
                dir('/var/www/html/Admin-Dashboard') {
                    sh 'yarn'  // Install dependencies
                    sh 'yarn run build' // Build the project
                }
            }
        }
        stage('Deploy') {
            steps {
                // sh 'pm2 restart admin' // Restart the PM2 process for the project
                // sh 'cp -r /var/www/html/Admin-Dashboard/build /var/www/Admin-Dashboard' // Copy new build to deployment directory
            }
        }
    }
}
