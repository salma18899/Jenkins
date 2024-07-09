pipeline {
    agent any

    stages {
        stage('Docker Compose Deployment') {
            steps {
                script {
                    sh '''
                        mongoDBstatus=$(docker ps -a --filter 'name=mongo' --format '{{.State}}')
                        mongoExpressStatus=$(docker ps -a --filter 'name=mongo-express' --format '{{.State}}')
                        
                        if [ "$mongoDBstatus" == "running" ]; then
                            echo "MongoDB is already running."
                        fi
                        
                        if [ "$mongoExpressStatus" == "running" ]; then
                            echo "Mongo Express is already running."
                        fi

                        if [ "$mongoDBstatus" != "running" ] || [ "$mongoExpressStatus" != "running" ]; then
                            echo "Docker Compose Up. Starting services..."
                            docker-compose up -d
                        else
                            echo "Both MongoDB and Mongo Express are already running. No need to start services."
                        fi
                    '''
                }
            }
        }
    }
}
