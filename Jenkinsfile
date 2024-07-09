pipeline {
    agent any
    stages {
        stage('Deploy Docker Compose') {
            steps {
                script {
                    // Bash script to check and handle the conditions
                    sh '''
                    #!/bin/bash

                    # Check if MongoDB is running and stop it
                    mongoRunning=$(docker ps --filter 'name=mongo' --format '{{.Names}}')
                    if [ ! -z "$mongoRunning" ]; then
                        docker stop $mongoRunning
                    fi

                    # Check if Mongo Express is running
                    mongoExpressStatus=$(docker ps -a --filter 'name=mongo-express' --format '{{.State}}')

                    if [ "$mongoExpressStatus" == "running" ]; then
                        echo "Mongo Express is already running."
                        exit 0
                    elif [ "$mongoExpressStatus" == "exited" ]; then
                        echo "Mongo Express is down. Starting services..."
                        docker-compose up -d
                    else
                        echo "Mongo Express does not exist. Starting services..."
                        docker-compose up -d
                    fi
                    '''
                }
            }
        }
    }
}
