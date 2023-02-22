pipeline {
    agent any
    triggers {
        cron('*/3 * * * *')
    }
    stages {
        // Build environment if this is the first run or if requirements have changed
        stage('Build') {
            when {
                anyOf {
                    equals(actual: currentBuild.number, expected: 1)
                    changeset "*requirements.txt"
                }          
            }
            steps {
                echo 'Building virtual environment'
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
        // Run code on every pipeline run
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