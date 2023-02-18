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
                sh 'mvn test'
            }
        }

        // stage('Integration testing'){

        //     steps{
        //         sh 'mvn verify -DskipTests'
        //     }
        // }

    }

}