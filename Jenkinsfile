pipeline{

    agent {
        docker {
            image 'maven:3.9.0-eclipse-temurin-11' 
            args '-v /root/.m2:/root/.m2' 
        }
    }

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

        stage('Maven version'){
            steps{
                sh "mvn test"
            }
        }

        stage('UNIT Testing'){

            steps{
                sh "mvn test"
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