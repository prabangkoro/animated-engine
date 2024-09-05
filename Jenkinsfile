pipeline {
    agent any
    options {
        skipDefaultCheckout()
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableConcurrentBuilds()
        timestamps()
        skipStagesAfterUnstable()
    }
    environment {
        DB_DRIVER = 'sqlite3'
        SECRET_SECRET = 'secret-key'
        TARGET_DEPLOYMENT = 'blue'
    }
    stages {
        stage('Init') {
            steps {
                echo "DB_DRIVER env is ${DB_DRIVER}"
                echo "SECRET_SECRET env is ${SECRET_SECRET}"
                sh 'printenv'
            }
        }
        stage('Build') {
            steps {
                echo 'Build done.'
            }
        }
        stage('Approval') {
            steps {
                timeout(time: 10, unit: 'SECONDS') {
                    script {
                        input(message: "Do you want to proceed deploy for ${TARGET_DEPLOYMENT} instance?")
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Proceed to deploy.'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
            deleteDir()
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}