pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                script {
                    // Checkout the Dev branch by default
                    git branch: 'Dev', 
                        url: 'https://github.com/Shk-Kaif/Kaif-Multibraches.git', 
                        credentialsId: 'Git-Pat'
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
                            configName: 'dev-server', // Correct server name for Dev
                            transfers: [
                                sshTransfer(
                                    sourceFiles: '**/*' // Adjust to your source files
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
        stage('Checkout UAT Code') {
            steps {
                script {
                    // Checkout the UAT branch
                    git branch: 'Uat',
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
                            configName: 'uat-server', // Correct server name for UAT
                            transfers: [
                                sshTransfer(
                                    sourceFiles: '**/*' // Adjust to your source files
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
        stage('Checkout Prod Code') {
            steps {
                script {
                    // Checkout the Prod branch
                    git branch: 'Prod',
                        url: 'https://github.com/Shk-Kaif/Kaif-Multibraches.git',
                        credentialsId: 'Git-Pat'
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
                            configName: 'prod-server', // Correct server name for Production
                            transfers: [
                                sshTransfer(
                                    sourceFiles: '**/*' // Adjust to your source files
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
            echo 'Pipeline completed.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
