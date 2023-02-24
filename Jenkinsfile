pipeline{

    agent any

    environment {
        SONAR_HOST_URL = "http://localhost:8094"
        SONAR_LOGIN = credentials('squ_b2d610b74d42d7dfacec9060e178280a2f3cb017')
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
                    sh 'mvn clean -DskipTests package sonar:sonar -Dsonar.login="${env.SONAR_LOGIN}" -Dsonar.host.url="${env.SONAR_HOST_URL}"'
                }
            }


        }
    }

}