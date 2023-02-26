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

        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv(installationName: 'sonarQube') {
                    sh 'mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=cicdMiniproject \
                        -Dsonar.host.url=http://localhost:8094 \
                        -Dsonar.login=sqp_aae3692a28b6fca645ce13c5028df1e2b3fb8571'
                }
            }


        }
    }

}