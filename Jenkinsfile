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
          pm2 delete my-app || true
          pm2 start server.js --name my-app
          pm2 save
          sleep 2
          pm2 logs my-app --lines 20 --nostream
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
