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
                    
                    
            }
        }
    }
}