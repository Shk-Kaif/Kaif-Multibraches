pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Replace 'github-creds' with your actual Jenkins credentials ID for GitHub
                git branch: "${BRANCH_NAME}", url: 'https://github.com/Shk-Kaif/Kaif-Multibraches.git', credentialsId: 'github-creds'
            }
        }

        stage('Deploy to UAT') {
            when {
                expression { return env.BRANCH_NAME == 'Uat' }  // Runs only if branch is Uat
            }
            steps {
                sshPublisher(publishers: [
                    sshPublisherDesc(
                        configName: 'uat-server',       // SSH configuration name for UAT server
                        transfers: [
                            sshTransfer(
                                sourceFiles: '*/',      // Files to transfer, adjust as needed
                                remoteDirectory: '/usr/share/nginx/html', // Directory on UAT server
                                execCommand: '''#!/bin/bash
                                    echo "Deploying to UAT server..."
                                    sudo systemctl reload nginx  # Reload Nginx after deploying
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
                expression { return env.BRANCH_NAME == 'Prod' }  // Runs only if branch is Prod
            }
            steps {
                sshPublisher(publishers: [
                    sshPublisherDesc(
                        configName: 'prod-server',       // SSH configuration name for Prod server
                        transfers: [
                            sshTransfer(
                                sourceFiles: '*/',      // Files to transfer, adjust as needed
                                remoteDirectory: '/usr/share/nginx/html', // Directory on Prod server
                                execCommand: '''#!/bin/bash
                                    echo "Deploying to Production server..."
                                    sudo systemctl reload nginx  # Reload Nginx after deploying
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
                expression { return env.BRANCH_NAME == 'Dev' }  // Runs only if branch is Dev
            }
            steps {
                sshPublisher(publishers: [
                    sshPublisherDesc(
                        configName: 'dev-server',       // SSH configuration name for Dev server
                        transfers: [
                            sshTransfer(
                                sourceFiles: '*/',      // Files to transfer, adjust as needed
                                remoteDirectory: '/usr/share/nginx/html', // Directory on Dev server
                                execCommand: '''#!/bin/bash
                                    echo "Deploying to Dev server..."
                                    sudo systemctl reload nginx  # Reload Nginx after deploying
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
