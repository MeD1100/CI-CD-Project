pipeline{

    agent any

    stages{

        stage('Git Checkout'){

            steps{
                git branch: 'main', url: 'https://github.com/MeD1100/CI-CD-Project.git'
            }
        }

        stage('UNIT Testing'){

            steps{
                sh(script: './mvnw --batch-mode -Dmaven.test.failure.ignore=true test')
            }
        }

        stage('Packaging'){

            steps{
                sh(script: './mvnw --batch-mode package -DskipTests')
            }
        }
    }
    post {
        always {
            junit(testResults: 'target/surefire-reports/*.xml', allowEmptyResults : true)
        }
    }

    }

}