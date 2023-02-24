pipeline{

    agent any

    tools{
        maven '3.9.0'
    }

    stages{

        stage('Git Checkout'){

            steps{
                git branch: 'main', url: 'https://github.com/MeD1100/CI-CD-Project.git'
            }
        }



        stage('Unit Testing'){
            steps{
                
                script{
                    withMaven(maven:'3.9.0'){
                        sh 'mvn test'
                    }
                }
            }
        }

        stage('Integration Testing'){

            steps{
                sh 'mvn verify -DskipUnitTests'
            }
        }

        stage('Maven Build'){
            steps{
                sh 'mvn clean install'
            }
        }

        stage('Creating mvnw file'){

        }

        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv(installationName: 'sonarserver') {
                    sh 'mvn clean org.sonarsource.scanner.maven:sonar-maven-plugin:4.8.0.2856:sonar'
                }
            }


        }
    }

}