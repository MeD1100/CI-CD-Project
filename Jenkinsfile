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
                    sh """${scannerHome}/bin/sonar-scanner \
                    -Dsonar.login=admin \
                    -Dsonar.password=21328166
                    -Dsonar.projectBaseDir=/var/jenkins_home/workspace/MiniProject/ \
                    -Dsonar.projectKey=testing \
                    -Dsonar.language=java
                    -Dsonar.sources=src/main/
                    -Dsonar.tests=src/test/
                    -Dsonar.host.url=http://localhost:8094/"""
                    }
            }
        }
    }

}