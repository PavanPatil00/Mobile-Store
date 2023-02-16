pipeline{
    agent any
    stages{
        stage ('checkout the code from SCM'){
            steps{
                echo 'checkout the code'
            }
        }
        stage ('Build the project'){
            steps{
                echo 'building the project'
                sh 'mvn clean install -DskipTests'
            }
        }
        stage('Sonarqube'){
            steps{
                 echo 'Sonar Codequality'
                 sh '''
                 mvn clean verify sonar:sonar \
                    -Dsonar.projectKey=Mobilestore \
                    -Dsonar.host.url=http://20.106.163.34:9000 \
                    -Dsonar.login=sqp_e4f289cfb9d1a08b38db8487183af0e60e676251
                    ''' 
            }
        }
        stage('buiding the docker image'){
            steps{
                 echo 'Docker image Build'
                 sh 'docker build -t mobilestore .'
        }
        }
        stage('Deploy to dev'){
            steps{
                echo "Deploying to dev environment"
                sh 'docker rm -f mobile || true'
                sh 'docker run -d --name=mobile -p 8099:8099 mobilestore'
            }
        }
    }
}