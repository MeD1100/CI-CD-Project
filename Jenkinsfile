pipeline{

    agent any

    stages{

        stage('Git Checkout'){

            steps{
                git branch: 'main', url: 'https://github.com/MeD1100/CI-CD-Project.git'
            }
        }

        stage('Java version'){
            steps{
                sh 'java --version'
            }
        }

        stage('UNIT Testing'){

            steps{
                withMaven(maven: 'Apache Maven 3.8.6') {
                    sh 'mvn test'
                }
            }
        }

        stage('Integration Testing'){

            steps{
                withMaven(maven: 'Apache Maven 3.8.6') {
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }

        stage('Maven Build'){
            steps{
                withMaven(maven: 'Apache Maven 3.8.6'){
                    sh 'mvn clean install'
                }
            }
        }

        stage('Sonarqube Analysis'){
            steps{
                script{
                    withMaven(maven: 'Apache Maven 3.8.6'){
                        withSonarQubeEnv(credentialsId: 'sonar-api') {
                            sh 'mvn clean package sonar:sonar'
                        }
                    }
                }
                
            }
        }
    }

}