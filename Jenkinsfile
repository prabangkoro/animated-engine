pipeline {
    agent any
    options {
        skipDefaultCheckout()
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableConcurrentBuilds()
        timestamps()
    }
    environment {
        DB_DRIVER = 'sqlite3'
        SECRET_SECRET = 'secret-key'
    }
    stages {
        stage('Build') {
            steps {
                echo "DB_DRIVER env is ${DB_DRIVER}"
                echo "SECRET_SECRET env is ${SECRET_SECRET}"
                sh 'printenv'
                echo 'Build done.'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
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