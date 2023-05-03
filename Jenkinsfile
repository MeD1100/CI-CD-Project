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
                    sh 'mvn clean verify sonar:sonar'
                    sh """/var/jenkins_home/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonarqube/bin/sonar-scanner \
                    -D sonar.projectVersion=1.0-SNAPSHOT \
                    -D sonar.login=admin \
                    -D sonar.password=21328166
                    -D sonar.projectBaseDir=/var/jenkins_home/workspace/MiniProject/ \
                        -D sonar.projectKey=project \
                        -D sonar.sourceEncoding=UTF-8 \
                        -D sonar.language=java \
                        -D sonar.sources=src/main \
                        -D sonar.tests=src/test \
                        -D sonar.host.url=http://localhost:8094/"""
                        }
            }
        }
    }

}