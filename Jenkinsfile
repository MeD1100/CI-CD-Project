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

        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonar-api') {
                    // Optionally use a Maven environment you've configured already
                    withMaven(maven:'Apache Maven 3.8.6') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
    }

}