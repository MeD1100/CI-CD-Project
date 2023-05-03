pipeline{

    agent any

    environment {
        scannerHome = tool 'SonarQube Scanner'
    }


    tools{
        maven '3.9.0'
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
                    withMaven(maven:'3.9.0'){
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

        // stage('SonarQube analysis') {
        //     steps {
        //         withSonarQubeEnv(installationName: 'sonarQube') {
        //             sh 'mvn clean verify sonar:sonar \
        //                 -Dsonar.projectKey=cicdMiniproject \
        //                 -Dsonar.host.url=http://localhost:8094 \
        //                 -Dsonar.login=sqp_aae3692a28b6fca645ce13c5028df1e2b3fb8571'
        //         }
        //     }


        // }

        stage('SonarQube Analysis') {
            def scannerHome = tool 'sonarqube'
            withSonarQubeEnv('sonarqube_token') {
            sh """/var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonarqube/bin/sonar-scanner \
            -D sonar.projectVersion=1.0-SNAPSHOT \
            -D sonar.login=admin \
            -D sonar.password=21328166 \
            -D sonar.projectBaseDir=/var/lib/jenkins/workspace/MiniProject/ \
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