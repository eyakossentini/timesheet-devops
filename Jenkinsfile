pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Fetch the code from the master branch of GitHub
                git branch: 'amira', url: 'https://github.com/eyakossentini/timesheet-devops.git'
            }
        }

        stage('Clean') {
            steps {
                // Clean the Maven project
                sh 'mvn clean '
            }
        }

        stage('Compile') {
            steps {
                // Compile the Maven project
                sh 'mvn compile'
            }
        }

        stage('Test Junit & Mockito'){
            steps{
                sh 'mvn test'
            }
        }

        stage('SonarQube analysis') {
            steps {
                // Exécution de l'analyse de code avec SonarQube
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }


    }

}

