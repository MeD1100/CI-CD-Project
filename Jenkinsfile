pipeline{

    agent any

    stages{

        stage('Git Checkout'){

            steps{
                git branch: 'main', url: 'https://github.com/MeD1100/CI-CD-Project.git'
            }
        }

        stage('Unit Testing'){
            steps{
                // Use the id of your globally configured maven instance
                def mvnTool = tool 'Apache Maven 3.8.6'

                // Execute Maven
                sh "${mvnTool}/bin/mvn test"
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

        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonar-api') {
                    // Optionally use a Maven environment you've configured already
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
    }

}