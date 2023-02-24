pipeline{

    agent any

    tools{
        maven '3.8.6'
        jdk 'JDK 1.8.0_51'
    }

    stages{

        stage('Git Checkout'){

            steps{
                git branch: 'main', url: 'https://github.com/MeD1100/CI-CD-Project.git'
            }
        }

        stage('Maven') {
            steps {
                sh "wget https://downloads.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz"
                sh "ls"
                sh "pwd"
                // sh "ls /home/jenkins/workspace/check"
                // sh "tar -xvzf /home/jenkins/workspace/check/apache-maven-3.6.3-bin.tar.gz"
                // sh "ls /home/jenkins/workspace/check/apache-maven-3.6.3/bin"
                // sh "export PATH==/home/jenkins/workspace/check/apache-maven-3.6.3/bin:$PATH"
                // sh "echo $PATH"
                // sh "mvn -version"
                
                //sh "sudo update-alternatives --install "/usr/bin/mvn" "mvn" "/opt/apache-maven-3.6.3/bin/mvn" 0"
                //sh "sudo update-alternatives --set mvn /opt/apache-maven-3.6.3/bin/mvn"
       }
        
    }

        stage('Unit Testing'){
            steps{
                
                script{
                    sh 'mvn test'
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

        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonar-api') {
                    // Optionally use a Maven environment you've configured already
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
    }

}