pipeline{

    agent any

    environment {
        scannerHome = tool 'sonarqube'
    }


    tools{
        maven '3.8.3'
    }

    stages{

        stage('Git Checkout'){

            steps{
                git branch: 'main', url: 'https://github.com/MeD1100/CI-CD-Project.git'
            }
        }



        // stage('Unit Testing'){
        //     steps{
                
        //         script{
        //             withMaven(maven:'3.8.3'){
        //                 sh 'mvn test'
        //             }
        //         }
        //     }
        // }

        // stage('Integration Testing'){

        //     steps{
        //         sh 'mvn verify -DskipUnitTests'
        //     }
        // }

        // stage('Maven Build'){
        //     steps{
        //         sh 'mvn clean install'
        //     }
        // }


        stage('SonarQube Analysis') {
            steps{
                withSonarQubeEnv('sonarqube_token') {
                    sh "mvn sonar:sonar -X"
                    }
            }
        }
    }

}