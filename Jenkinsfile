pipeline {

    stages {
        stage('Docker login'){
            agent { label 'worknode1'}
            steps{
                sh 'docker login -u amjadgondal --password "@mj@d@31o6"'
            }
        }
        stage('Docker Build') {
            agent { label  'worknode1'}
            steps {
                sh 'docker build -t amjadgondal/webapp:latest .'
            }
        }
        stage('Docker Push') {
            agent { label  'worknode1'}
            steps {
                    sh 'docker push amjadgondal/webapp:latest'  
            }
        }

        stage('CD Stage') {
            agent { label  'worknode1'}
            steps {
                    sh '''
                    docker kill nginx-image
                    docker run -d --rm -p 8200:80 --name nginx-image amjadgondal/webapp:latest
                    '''
            }
        }
    }
}
