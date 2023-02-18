pipeline{

    agent any

    tools{
        maven "Maven_3.8.6"
        jdk "JDK 9"
    }

    stages{

        stage('Git Checkout'){

            steps{
                git branch: 'main', url: 'https://github.com/MeD1100/CI-CD-Project.git'
            }
        }

        stage('UNIT Testing'){

            steps{
                tool 'Maven_3.8.6'
                sh 'mvn test'
            }
        }

        stage('Integration testing'){

            steps{
                tool 'Maven_3.8.6'
                sh 'mvn verify -DskiUnitTests'
            }
        }

    }

}