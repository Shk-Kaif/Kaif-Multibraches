pipeline {
    agent any
    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'Uat', description: 'Branch to deploy')
    }
    stages {
        stage('Checkout Code') {
            steps {
                script {
                    // Ensure Git credentials are specified
                    git branch: "${params.BRANCH_NAME}",
                        url: 'https://github.com/Shk-Kaif/Kaif-Multibraches.git',
                        credentialsId: 'Git-Pat'
                }
            }
        }
        stage('Deploy to UAT') {
            steps {
                script {
                    echo 'Deploying to UAT...'

                    // Publish Over SSH for UAT
                    sshPublisher(publishers: [
                        sshPublisherDesc(
                            configName: 'uat-server', 
                            transfers: [
                                sshTransfer(
                                    sourceFiles: '**/*' // No remote directory specified
                                )
                            ],
                            usePromotionTimestamp: false,
                            useWorkspaceInPromotion: false,
                            useWorkspaceInProduction: false
                        )
                    ])
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to Production...'

                    // Publish Over SSH for Production
                    sshPublisher(publishers: [
                        sshPublisherDesc(
                            configName: 'prod-server',
                            transfers: [
                                sshTransfer(
                                    sourceFiles: '**/*' // No remote directory specified
                                )
                            ],
                            usePromotionTimestamp: false,
                            useWorkspaceInPromotion: false,
                            useWorkspaceInProduction: false
                        )
                    ])
                }
            }
        }
        stage('Deploy to Dev') {
            steps {
                script {
                    echo 'Deploying to Dev...'

                    // Publish Over SSH for Dev
                    sshPublisher(publishers: [
                        sshPublisherDesc(
                            configName: 'dev-server',
                            transfers: [
                                sshTransfer(
                                    sourceFiles: '**/*' // No remote directory specified
                                )
                            ],
                            usePromotionTimestamp: false,
                            useWorkspaceInPromotion: false,
                            useWorkspaceInProduction: false
                        )
                    ])
                }
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
