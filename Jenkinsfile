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
                        println powershell(returnStdout: true, script: 'rm -r venv')
                    }
                    println powershell(returnStdout: true, script: '''
                            python -m venv venv
                            venv/scripts/activate
                            pip install -r requirements.txt
                        '''
                    )
                }
            }
        }
        stage('Run') {
            steps {
                echo 'Running'
                script {
                    println powershell(returnStdout: true, script: '''
                            venv/scripts/activate
                            python main.py
                        '''
                    )
                }
            }
        }
    }
}