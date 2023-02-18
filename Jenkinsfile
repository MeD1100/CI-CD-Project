pipeline{

    agent any
    tools { 
      maven 'MAVEN_HOME' 
      jdk 'JAVA_HOME' 
    }

    stages{

        stage('Git Checkout'){

            steps{
                git branch: 'main', url: 'https://github.com/MeD1100/CI-CD-Project.git'
            }
        }

        stage('UNIT Testing'){

            steps{
                sh 'mvn test'
            }
        }

        stage('Integration testing'){

            steps{
                sh 'mvn verify -DskiUnitTests'
            }
        }

    }

}