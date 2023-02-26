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

    }
    
    post {
        always {
            script {
                def scannerHome = tool 'SonarQube Scanner'
                withSonarQubeEnv('sonarQube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }

            script {
                def issuesReportFilePath = 'target/sonar/issues-report/issues-report.json'
                def taskReportFilePath = 'target/task-report.txt'

                // Convert SonarQube issues report to task report format
                sh "npx sonarqube-to-task-report --input ${issuesReportFilePath} --output ${taskReportFilePath}"
            }

            script {
                def serverUrl = "http://localhost:8094"
                def credentialsId = "sqp_aae3692a28b6fca645ce13c5028df1e2b3fb8571"
                def projectKey = "cicdMiniproject"
                def projectVersion = "1.0.1"

                withSonarQubeEnv('sonarQube') {
                    // Publish analysis results and generate task report
                    sh "sonar-scanner -Dsonar.host.url=${serverUrl} -Dsonar.login=\$${credentialsId} -Dsonar.projectKey=${projectKey} -Dsonar.projectVersion=${projectVersion} -Dsonar.report.export.path=task-report.txt"
                }
            }
        }
    }

}