pipeline {
    agent any
    triggers {
        cron('*/3 * * * *')
    } 
    stages {
        stage('Pull changes') {
            when {
                changeset "*"
            }
            steps {
                echo 'Merging changes'
                script {
                    echo "Changeset: ${currentBuild.changeSets}"
                }
            }
        }
        stage('Build') {
            when {
                    changeset "*requirements.txt"             
            }
            steps {
                echo 'Rebuilding because requirements changed'
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