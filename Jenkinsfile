pipeline {
    agent any
    triggers {
        cron('*/3 * * * *')
    } 
    stages {
        stage('Build') {
            when {
                changeset "*"
            }
            steps {
                echo 'Executing build because changes were detected'
                script {
                    echo "Changeset: ${currentBuild.changeSets}"
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