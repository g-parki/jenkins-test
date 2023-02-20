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
                        def del_venv = powershell(returnStdout: true, script: 'rm -r venv')
                        println del_venv
                    }
                    def create_venv = powershell(returnStdout: true, script: '''
                            python -m venv venv
                            venv/scripts/activate
                            pip install -r requirements.txt
                        '''
                    )
                    println create_venv
                }
            }
        }
        stage('Run') {
            steps {
                echo 'Running'
                script {
                    def run = powershell(returnStdout: true, script: '''
                            venv/scripts/activate
                            python main.py
                        '''
                    )
                    println run
                }
            }
        }
    }
}