pipeline {
    agent any
 
    stages {
        stage('Build'){
            steps {
                sh 'curl -sL https://deb.nodesource.com/setup_14.x | bash -'
                sh 'apt-get install nodejs -y'
                sh 'npm install --global --force yarn'

                sh 'git pull'
                sh 'yarn'
                sh 'yarn build:linux'
            }
            post {
                always {
                    echo "Build stage finished";
                }
                success{
                    echo "Build Success";
                }
                failure {
                    echo "Build Failure";
                    mail body: "Please visit jenkins for further information", subject: "Build failed", to: "annagrzesiak04@gmail.com";
                }
            }
        }
        stage('Test') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                sh 'yarn test'
                
            }

            post {
                always {
                    echo "Test stage finished";
                }
                success{
                    echo "Test Success";
                }
                failure {
                    echo "Test Failure";
                    mail body: "Please visit jenkins for further information", subject: "Build failed", to: "annagrzesiak04@gmail.com";
                }
            }
        }
    }
    
}
