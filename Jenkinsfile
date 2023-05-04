pipeline{

    agent any

    // environment {
    //     scannerHome = tool 'sonarqube'
    // }


    tools{
        maven '3.8.3'
        scannerHome 'sonarqube'
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
                    sh """{$scannerHome}/bin/sonar-scanner \
                    -Dsonar.login=squ_c52711341143682d62eb26e9b7bb5653ba83f404 \
                    -Dsonar.projectKey=testing \
                    -Dsonar.host.url=http://localhost:9000"""
                    }
            }
        }
    }

}