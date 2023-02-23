pipeline{

    agent any
    tools{
        maven 'Apache Maven 3.8.6'
    }

    stages{

        stage('Git Checkout'){

            steps{
                git branch: 'main', url: 'https://github.com/MeD1100/CI-CD-Project.git'
            }
        }

        stage('Java version'){
            steps{
                bat 'java --version'
            }
        }

        stage('Maven version'){
            steps{
                def mvnHome = tool 'Apache Maven 3.8.6'
                bat "${mvnHome}/bin/mvn test"
            }
        }

        stage('UNIT Testing'){

            steps{
                bat "mvn test"
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