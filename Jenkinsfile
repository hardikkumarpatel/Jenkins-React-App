pipeline {
    agent any
    stages {
        stage('Checkout Latest Code') {
            steps {
                echo "Inside the checkout...";
                dir('/root/var/www/html/React-App-Demo') {
                    sh 'git checkout master' // Ensure we are on master branch
                    sh 'git pull origin master' // Pull latest code from remote
                }
            }
        }
        stage('Clean Previous Build') {
            echo "Inside the clean build...";
            steps {
                dir('/root/var/www/html/React-App-Demo') {
                    sh 'rm -rf build' // Remove old build directory
                }
            }
        }
        stage('Install Dependencies & Build') {
            echo "Inside the build installation...";
            steps {
                dir('/root/var/www/html/React-App-Demo') {
                    sh 'yarn'  // Install dependencies
                    sh 'yarn run build' // Build the project
                }
            }
        }
        // stage('Deploy') {
        //     steps {
        //         // sh 'pm2 restart admin' // Restart the PM2 process for the project
        //         // sh 'cp -r /var/www/html/React-App-Demo/build /var/www/React-App-Demo' // Copy new build to deployment directory
        //     }
        // }
    }
}
