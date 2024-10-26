pipeline {
    agent any

    environment {
        BRANCH_NAME = "${env.GIT_BRANCH ?: 'main'}"  // Dynamically assign branch name
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout from the specified branch
                git branch: "${BRANCH_NAME}", url: 'https://github.com/Shk-Kaif/Kaif-Multibraches.git'
            }
        }

        stage('Deploy to UAT') {
            when {
                expression { return BRANCH_NAME == 'origin/Uat' }  // Ensure branch check matches remote branch name
            }
            steps {
                sshPublisher(publishers: [
                    sshPublisherDesc(
                        configName: 'uat-server',
                        transfers: [
                            sshTransfer(
                                sourceFiles: '**/*',  // Adjusted to match all files
                                removePrefix: '',     
                                remoteDirectory: '/usr/share/nginx/html',
                                execCommand: '''
                                    echo "Deploying to UAT server..."
                                    sudo systemctl reload nginx
                                    echo "Deployment to UAT server complete."
                                '''
                            )
                        ],
                        verbose: true
                    )
                ])
            }
        }

        stage('Deploy to Production') {
            when {
                expression { return BRANCH_NAME == 'origin/Prod' }
            }
            steps {
                sshPublisher(publishers: [
                    sshPublisherDesc(
                        configName: 'prod-server',
                        transfers: [
                            sshTransfer(
                                sourceFiles: '**/*',
                                remoteDirectory: '/usr/share/nginx/html',
                                execCommand: '''
                                    echo "Deploying to Production server..."
                                    sudo systemctl reload nginx
                                    echo "Deployment to Production server complete."
                                '''
                            )
                        ],
                        verbose: true
                    )
                ])
            }
        }

        stage('Deploy to Dev') {
            when {
                expression { return BRANCH_NAME == 'origin/Dev' }
            }
            steps {
                sshPublisher(publishers: [
                    sshPublisherDesc(
                        configName: 'dev-server',
                        transfers: [
                            sshTransfer(
                                sourceFiles: '**/*',
                                remoteDirectory: '/usr/share/nginx/html',
                                execCommand: '''
                                    echo "Deploying to Dev server..."
                                    sudo systemctl reload nginx
                                    echo "Deployment to Dev server complete."
                                '''
                            )
                        ],
                        verbose: true
                    )
                ])
            }
        }
    }
}
