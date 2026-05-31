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