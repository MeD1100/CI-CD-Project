pipeline{

    agent any

    tools{
        maven "Apache Maven 3.8.6"
        jdk "Java11"
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

        stage('UNIT Testing'){

            steps{
                tool 'Apache Maven 3.8.6'
                sh 'mvn test'
            }
        }

        stage('Integration testing'){

            steps{
                tool 'Apache Maven 3.8.6'
                sh 'mvn verify -DskipTests'
            }
        }

    }

}