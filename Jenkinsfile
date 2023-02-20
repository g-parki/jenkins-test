pipeline {
    agent any
    triggers {
        cron('*/3 * * * *')
    } 
    stages {
        stage('Stage 1') {
            steps {
                echo 'Hello world!' 
            }
        }
    }
}