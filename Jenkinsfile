pipeline {
    agent any
    stages {
        stage('Checkout Latest Code') {
            steps {
               script {
                    sh 'git config --global --add safe.directory "/var/lib/jenkins/workspace/NJP Automation"'
                }
                    sh 'git checkout master' // Ensure we are on master branch
                    sh 'git pull origin master' // Pull latest code from remote
            }
        }
        stage('Clean Previous Build') {
            steps {
                    sh 'rm -rf build' // Remove old build directory
            }
        }
        stage('Install Dependencies & Build') {
            steps {
                    sh 'yarn'  // Install dependencies
                    sh 'yarn run build' // Build the project
            }
        }
        stage('Deploy') {
            steps { 
              echo "Deployed successfully..." 
            }
        }
    }
}
