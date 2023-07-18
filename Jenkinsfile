pipeline {
    agent any
    stages {
        
        stage('Docker Build') {
            agent { label  'worknode1'}
            steps {
                sh 'docker build -t amjadgondal/mywebapp:latest .'
            }
        }
        

        stage('CD Stage') {
            agent { label  'worknode1'}
            steps {
                    sh '''
                    docker kill nginx-image
                    docker run -d --rm -p 8200:80 --name nginx-image amjadgondal/mywebapp:latest
                    '''
            }
        }
    }
}
