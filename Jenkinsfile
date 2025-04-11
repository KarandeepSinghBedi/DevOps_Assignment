pipeline {
    agent {
        any
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-org/your-repo.git'
            }
        }
        stage('Build') {
            steps {
                // Example: Build a Java project with Maven
                sh 'mvn clean install -DskipTests'
            }
        }
        stage('Test') {
            steps {
                // Example: Run unit tests
                sh 'mvn test'
            }
        }
        stage('Deploy to Staging') {
            steps {
                // Example: Deploy to a staging server
                sh 'echo "Deploying to staging..."'
            }
            post {
              failure {
                 echo 'Staging Deployment Failed'
              }
              success {
                 echo 'Staging Deployment Succeeded'
              }
            }
        }
        stage('Input for Production Deployment') {
            input {
                message "Proceed to deploy to production?"
                ok "Yes, deploy!"
            }
        }
        stage('Deploy to Production') {
            steps {
                // Example: Deploy to the production server
                sh 'echo "Deploying to production..."'
            }
             post {
              failure {
                 echo 'Production Deployment Failed'
              }
              success {
                 echo 'Production Deployment Succeeded'
              }
            }
        }
    }
    //Handle failures in pipeline
    post {
        failure {
            mail to: 'karandeepsinghbedi@gmail.com',
                 subject: "Pipeline Failed",
                 body: "Pipeline ${env.JOB_NAME} build ${env.BUILD_NUMBER} failed.  See ${env.BUILD_URL} for details."
        }
        success {
             mail to: 'karandeepsinghbedi@gmail.com',
                 subject: "Pipeline Succeeded",
                 body: "Pipeline ${env.JOB_NAME} build ${env.BUILD_NUMBER} succeeded.  See ${env.BUILD_URL} for details."
        }
    }
}
