pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                script {
                    // Ensure Git credentials are specified
                    git branch: 'Uat', // Change this to the desired branch if needed
                        url: 'https://github.com/Shk-Kaif/Kaif-Multibraches.git',
                        credentialsId: 'Git-Pat'
                }
            }
        }
        stage('Deploy to UAT') {
            steps {
                // Add your deployment logic for UAT here
                echo 'Deploying to UAT...'
            }
        }
        stage('Deploy to Production') {
            steps {
                // Add your deployment logic for Production here
                echo 'Deploying to Production...'
            }
        }
        stage('Deploy to Dev') {
            steps {
                // Add your deployment logic for Dev here
                echo 'Deploying to Dev...'
            }
        }
    }
    post {
        always {
            // Actions to perform after the pipeline finishes
            echo 'Pipeline completed.'
        }
        failure {
            // Actions to perform if the pipeline fails
            echo 'Pipeline failed.'
        }
    }
}
