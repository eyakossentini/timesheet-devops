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
                    sh 'mvn sonar:sonar \
                          -Dsonar.projectKey=timesheet_devops \
                          -Dsonar.host.url=http://192.168.50.4:9000 \
                          -Dsonar.login=87e68540f4c4d18923890704ee5fbd4c5ffbbe3f'
                }
            }
        }
         stage('Deploy to Nexus') {
                    steps {
                        // Étape de déploiement vers Nexus en sautant les tests
                        sh 'mvn deploy -DskipTests'
                    }
                }
            


    }

}

