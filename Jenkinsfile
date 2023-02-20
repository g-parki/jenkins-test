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
                        def output = powershell(returnStdout: true, script: '''
                            rm -r venv
                            python -m venv venv
                            '''
                        )
                        println output
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