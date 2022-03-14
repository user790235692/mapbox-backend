pipeline {
    agent any

    stages {
        stage('Configure project for dev') {
            when{
                branch 'dev'
            }
            steps {
                echo 'Configure the project'
                sh 'ls -la'
                sh 'cp /home/fedora/.credentials/.env /var/lib/jenkins/workspace/mapbox-backend_dev'
            }
        }

        stage('Configure project for main') {
            when{
                branch 'main'
            }
            steps {
                echo 'Configure the project'
                sh 'ls -la'
                sh 'cp /home/fedora/.credentials/.env /var/lib/jenkins/workspace/mapbox-backend_main'
            }
        }

        stage('Buil') {
            steps {
                echo 'Building..'
                sh 'npm i'
                sh 'docker-compose up -d'
                sh 'sleep 20'
                sh 'npx prisma migrate dev --name init'
                
            }
        }

        stage('Test') {
            steps {
                echo 'Test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying....'
                echo 'Delete the older version'
                sh 'rm -rf /var/www/mapbox-backend'
                sh 'cp -R /var/lib/jenkins/workspace/mapbox-backend_main /var/www'
                sh 'mv /var/www/mapbox-backend_main /var/www/mapbox-backend' 
            }
        }
    }
}