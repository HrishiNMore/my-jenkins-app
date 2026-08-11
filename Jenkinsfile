pipeline {
    agent any

    parameters {
        string(name: 'PORT', defaultValue: '3000', description: 'Port to run app on')
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Code already checked out by Jenkins SCM step'
            }
        }

        stage('Install') {
            steps {
                sh 'node -v'
                sh 'npm install'
            }
        }

        stage('Run') {
            steps {
                sh '''
                  pkill -f "node server.js" || true
                  nohup npm start > app.log 2>&1 &
                  sleep 2
                  cat app.log
                '''
            }
        }
    }

    post {
        success {
            echo "App deployed on port ${params.PORT}"
        }
        failure {
            echo 'Build failed — check console output'
        }
    }
}
