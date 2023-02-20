pipeline {
    agent any
    triggers {
        cron('*/3 * * * *')
    } 
    stages {

        stage('Build') {
            when {
                    changeset "*requirements.txt"             
            }
            steps {
                echo 'Rebuilding because requirements changed'
                script {
                    if (fileExists('venv')) {
                        powershell '''rm -r venv'''
                        echo 'venv deleted'
                        powershell '''python -m venv venv'''
                    }
                }
            }
        }
        stage('Run') {
            steps {
                echo 'Running'
                script {
                    echo "${currentBuild.changeSets}"
                }
            }
        }
    }
}