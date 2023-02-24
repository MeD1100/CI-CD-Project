pipeline{

    agent any

    tools{
        maven '3.8.6'
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
                    // Use the id of your globally configured maven instance
                    sh '"C:/Program Files/apache-maven-3.8.6/bin/mvn" test'
                }
            }
        }

        stage('Integration Testing'){

            steps{
                sh '"C:/Program Files/apache-maven-3.8.6/bin/mvn" verify -DskipUnitTests'
            }
        }

        stage('Maven Build'){
            steps{
                sh '"C:/Program Files/apache-maven-3.8.6/bin/mvn" verify -DskipUnitTests'
            }
        }

        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonar-api') {
                    // Optionally use a Maven environment you've configured already
                    sh '"C:/Program Files/apache-maven-3.8.6/bin/mvn" clean package sonar:sonar'
                }
            }
        }
    }

}