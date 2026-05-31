pipeline{
    agent any
    tools{
        maven "Maven"
    }
    stages{
        stage('Checkout'){
            steps{
                git branch: 'main',
                url: 'https://github.com/sarthak-agnihotri/employee-app.git'
            }
        }
        stage('Build JAR'){
            steps{
                bat 'mvn clean package'
            }
        }
        stage('Build Docker Image'){
            steps{
                bat 'docker build -t employeeapp .'
            }
        }
        stage('Docker Login') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                }
            }
        }
        stage('Push Image'){
            steps{
                bat 'docker tag employeeapp sarthak0144/employeeapp:v2'
                bat 'docker push sarthak0144/employeeapp:v2'
            }
        }
        stage('Run Container'){
            steps{
                bat 'docker rm -f employeecontainer || exit 0'
                bat 'docker run --name employeecontainer employeeapp'
            }
        }
    }
    post {

        success {

            echo 'Pipeline Successful'

        }

        failure {

            echo 'Pipeline Failed'

        }

        always {

            echo 'Pipeline Finished'

        }

    }
}
//push to docker hub
// docker tag localImage username/repository:tag
// docker push username/repository:tag
// docker pull username/repository:tag
// java -jar target/employee-app-4.0.0.jar see the jar file
//mvn clean package to build the jar file
