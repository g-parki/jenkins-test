pipeline {
    agent any
    triggers {
        cron('*/3 * * * *')
    } 
    stages {
        stage('Something changed, but not requirements') {
            when {
                allOf {
                    changeset "*"
                    changeset "[!requirements.txt]"
                }
                
            }
            steps {
                echo 'Executing build because changes were detected'
                script {
                    echo "Changeset: ${currentBuild.changeSets}"
                }
            }
        }
        stage('Requirements changed') {
            when {
                allOf {
                    changeset "*requirements.txt"
                }
                
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