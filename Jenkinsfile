pipeline{

    agent any

    tools{
        maven '3.8.6'
        jdk 'JDK1.8.0_51'
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
                    withMaven(maven:'3.8.6'){
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