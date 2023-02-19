pipeline {
    agent any
    triggers {
        cron('*/5 * * * *')
    } 
    stages {
        stage('Stage 1') {
            steps {
                echo 'Hello world!' 
            }
        }
    }
}